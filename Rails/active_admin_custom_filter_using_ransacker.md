# 개요
ActiveAdmin의 custom filter를 ransacker를 이용하여 제공해보자.<br/>
모델의 association attribute로 검색하거나 더 복잡한 조건문을 달아 필터링 할 때 유용하다.<br/>

# How to?
사용자(user)와 카드(card)는 has_many 관계이고, 등록한 카드 종류로 사용자를 필터링 하는 기능을 구현한다고 가정하자.<br/>
ransacker의 formatter에 filtered base를 만들어줌으로써 custom filter를 만들 수 있다.

```ruby
# admin/user.rb

filter :user_by_card_category_in, as: :string, label: '등록한 결제 수단 ID'
```
> **filter의 postfix는 in 이어야 한다.** <br/>
ransacker에 의해 필터링 되는 레코드의 전부를 보여줄 것이기 때문이다.<br/>
equals로 하면 아무런 결과도 나오지 않음!(card_category = [1,2,3] 인건 없을테니까)

```ruby
# User.rb

ransacker :user_by_card_category, formatter: proc { |v|
  card_ids = Card.joins(:user).where(users: {card_category = v}).pluck(:id)
  data = User.where(card_id: card_ids).pluck(:id)
  data.presence
} do |parent|
  parent.table[:id]
end
```


<hr/>

## 참고
- http://nikhgupta.com/code/activeadmin/custom-filters-using-ransacker-in-activeadmin-interfaces/
