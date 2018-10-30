# Rails에서 N:N Relation 생성하기!

## 문제 상황 가정
가게 주인(Owner)과 종업원(Staff)가 있다. 

이중 취업도 가능하며, 한 가게에는 여러 명의 종업원이 일할 수 있고, 한 종업원은 여러 가게에서 일할 수 있다고 해보자.

두 모델(Owner, Staff)은 N:N의 관계로 엮어야 한다.

## N:N Relation
이 때, 두 가지 방법이 있다.

1. rails 가이드에서 제공하는 [has_and_belongs_to_many](https://guides.rubyonrails.org/association_basics.html#the-has-and-belongs-to-many-association) 를 쓰거나, 

2. 직접 중간 테이블을 만들어서 N:1-1:N의 관계를 만들어주는 방법!

`has_and_belongs_to_many`도 내부적으로는 N:1-1:N을 위한 테이블을 만든다. 

다만 차이점은 ActiveRecord 모델을 만들지 않는다는것. 그렇기에 확장성이 떨어진다.

## 어떤 경우에 [has_and_belongs_to_many](https://guides.rubyonrails.org/association_basics.html#the-has-and-belongs-to-many-association)를 써야 할까?
두 테이블 간의 관계가 맺고 끊어지는 것만 필요할 때 사용!

## 어떤 경우에 직접 조인용 테이블을 만들어야 할까?
두 테이블 간의 관계가 맺고 끊어지는 것 외에 부가 정보를 저장해야 할 때 사용!

```ruby
class Owner < ActiveRecord
  has_many :owner_staffs
  has_many :staffs, through: :owner_staffs, source: :staff
  
  # 이하 생략
end

class Staff < ActiveRecord
  has_many :owner_staffs
  has_many :owners, through: :owner_staffs, source: :owner
  
  # 이하 생략
end

# == Schema Information
# id          :integer
# owner_id    :integer
# staff_id    :integer
# manageable  :boolean
class OwnerStaff < ActiveRecord
  belongs_to :staff
  belongs_to :owner
  
  # 이하 생략  
end
```

이러한 쿼링이 가능해진다.
```ruby
> owner = Owner.first
> owner.staffs
SELECT `staffs`.* FROM `staffs` INNER JOIN `owner_staffs` ON `staffs`.`id` = `owner_staffs`.`staff_id` WHERE `owner_staffs`.`owner_id` = 1
```
