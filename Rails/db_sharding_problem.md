# 환경
DB sharding을 위해 [Octopus](https://github.com/thiagopradi/octopus)라는 gem을 사용 중에 있음.

# 문제
한 테이블에 대해 update 후 select를 했으나 빈 결괏값이 나옴.
```SQL
UPDATE coupon_instances SET user_id = 1 where id = 2; # succeeded
SELECT * from coupon_instances where user_id = 1;     # empty result
```
현상을 살펴보니 로컬에서는 잘 결괏값이 나오지만, 알파 환경에서만 나오지 않고 있음.

# 해결
1. 엄청난 삽질 끝에, sharding과 관련있지 않을까 라는 생각이 문들 들게 됨.
  
   > master-slave 간의 동기화에 시간이 걸리는게 아닐까?

2. 로컬에서는 정상동작하는데 알파에선 왜 이상동작을 하는지 생각해보니, sharding은 알파 이상의 환경에서만 동작하고 있음.
3. `update - select`를 모두 master에서 하도록 코드 수정
```ruby
Octopus.using(:master) do
  CouponInstance.find(2).update(user_id: 1)
  CouponInstance.where(user_id: 1)
end
```

- 참고: https://github.com/thiagopradi/octopus/wiki/sharding
