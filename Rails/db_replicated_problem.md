# 환경
DB replicate 위해 [Octopus](https://github.com/thiagopradi/octopus)라는 gem을 사용 중에 있음.

# 문제
한 테이블에 대해 update 후 select를 했으나 빈 결괏값이 나옴.
```SQL
UPDATE coupon_instances SET user_id = 1 WHERE id = 2; # succeeded
SELECT * FROM coupon_instances WHERE user_id = 1;     # empty result
```
현상을 살펴보니 로컬에서는 잘 결괏값이 나오지만, 알파 환경에서만 나오지 않고 있음.

# 해결
1. 엄청난 삽질 끝에, **sharding/replicate과 관련있지 않을까?** 라는 생각이 문득 들게 됨.
  
   > master-slave 간의 동기화에 시간이 걸리는게 아닐까?

2. 로컬에서는 정상동작하는데 알파에선 왜 이상하게 동작하는지 생각해보니, replicate는 알파 이상의 환경에서만 설정 및 동작하고 있음.
3. `update - select`를 모두 master에서 하도록 코드 수정
```ruby
Octopus.using(:master) do
  CouponInstance.find(2).update(user_id: 1)
  CouponInstance.where(user_id: 1)
end
```

##참고
- https://github.com/thiagopradi/octopus/wiki/Replication
- https://github.com/thiagopradi/octopus/wiki/sharding
- https://github.com/thiagopradi/octopus/wiki/config-file
- https://github.com/aria-grande/TIL/blob/master/DB/shard_replication.md

# 앗!
shard/replication 문제가 아닐 수도 있다.
알파 환경의 master/slave는 같은 노드를 바라보고 있음. 그럼 동기화와 크게 관련이 없을텐데..

- 문제 상황 코드의 로그(edited query log로 정확하게 동작하는 쿼리가 아닙니다)
```ruby
CouponInstance.update
CouponInstance.select
```
```SQL
[Shard: slave]  CouponTemplate Load (7.1ms)  SELECT  `coupon_templates`.* FROM `coupon_templates` WHERE (blahblahcondition) LIMIT 1
[Shard: slave]  CouponInstance Load (5.0ms)  SELECT `coupon_instances`.* FROM `coupon_instances` WHERE  `coupon_instances`.`user_id` = '1'
[Shard: slave]  CouponInstance Load (7.7ms)  SELECT  `coupon_instances`.* FROM `coupon_instances` WHERE `coupon_instances`.`template_id` = 2 LIMIT 1
   (7.1ms)  SAVEPOINT active_record_1
  CouponTemplate Load (6.4ms)  SELECT `coupon_templates`.* FROM `coupon_templates` WHERE `coupon_templates`.`id` = 2 LIMIT 1
  CouponInstance Exists (6.7ms)  SELECT  1 AS one FROM `coupon_instances` WHERE `coupon_instances`.`user_id` = BINARY '1' AND `coupon_instances`.`id` != 1212 LIMIT 1
  SQL (6.7ms)  UPDATE `coupon_instances` SET `user_id` = '1' WHERE `coupon_instances`.`id` = 1212
   (8.0ms)  RELEASE SAVEPOINT active_record_1
[Shard: slave]  SQL (10.7ms)  SELECT `coupon_instances`.* FROM `coupon_instances` WHERE `coupon_instances`.`user_id` = '1'
   (20.8ms)  COMMIT
```


- 한 트랜잭션으로 묶었을 경우
```ruby
CouponInstance.transaction do
  CouponInstance.update
  CouponInstance.select
end
```
```SQL
  CouponTemplate Load (9.7ms)  CouponTemplate Load (7.1ms)  SELECT  `coupon_templates`.* FROM `coupon_templates` WHERE (blahblahcondition) LIMIT 1
  CouponInstance Load (5.0ms)  SELECT `coupon_instances`.* FROM `coupon_instances` WHERE  `coupon_instances`.`user_id` = '1'
  CouponInstance Load (6.6ms)  CouponInstance Load (7.7ms)  SELECT  `coupon_instances`.* FROM `coupon_instances` WHERE `coupon_instances`.`template_id` = 2 LIMIT 1
   (12.0ms)  SAVEPOINT active_record_1
  CouponTemplate Load (7.4ms)  SELECT  `coupon_templates`.* FROM `coupon_templates` WHERE `coupon_templates`.`id` = 2 LIMIT 1
  CouponInstance Exists (7.8ms)  SELECT  1 AS one FROM `coupon_instances` WHERE `coupon_instances`.`user_id` = BINARY '1' AND `coupon_instances`.`id` != 1212 LIMIT 1
  SQL (8.1ms)  UPDATE `coupon_instances` SET `user_id` = '1' WHERE `coupon_instances`.`id` = 1212
   (7.6ms)  RELEASE SAVEPOINT active_record_1
  SQL (12.4ms)  SELECT `coupon_instances`.* FROM `coupon_instances` WHERE `coupon_instances`.`user_id` = '1'
   (32.9ms)  COMMIT
```

트랜잭션으로 묶으면 모두 마스터에서 쿼리 실행!
즉, `Octopus.using(:master)`와 같게 동작하는 것.
