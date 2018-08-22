# Learn and Run ruby!

## Introduction
Ruby is the interpreted scripting language for quick and easy object-oriented programming. 

It is simple, straight-forward, and extensible.

Everything is an object in ruby, since it is pure object-oriented language.

## Documentation
- [Official Ruby Github](https://github.com/ruby/ruby)
- [Tutorial Documentation](https://www.ruby-lang.org/ko/)
- [Probramming Ruby, ebook](http://ruby-doc.com/docs/ProgrammingRuby/)

## Characteristics
### No semi-colon`;`
### NULL is nil
```ruby
init_value = nil
```

### Sys out
```ruby
puts "This output is for debugging"
```

### Symbol
- Also an object.
- But, Immutable!
```ruby
key = :name
key += 'hehe' # undefined method '+' for symbol

key = :new_name # succeed
```
- Symbol is used for key in hash.
- stored in heap memory, and reusable.
- managed via Symbol Dictionary
```ruby
Symbol.all_symbols
```

## Variable
### Dynamically typed
```ruby
# instead of `int score = 20;`
score = 20
```
### Wide variable scope
```ruby
score = 100
@score = 100
@@score = 100
$score = 100
```
- local variable
- instance variable
- class variable
- global variable

substituting Variables into Strings
```ruby
variable = 'b'
"a#{variable}c" # 'abc'
```

## Data structures 
### String
```ruby
'This is string'
```
### Array/List
```ruby
a_scores = [20, 40, 50]
b_scores = [20, 30]

a_scores[0] # 20
a_scores.first # 20
a_scores.last # 50
a << 60 # [20, 40, 50, 60]
```
- iterate
```ruby
scores = [20, 30, 40, 50]
scores.each do |score|
  # do something
end
```

- 어떻게 될까?
```
a_scores - b_scores
```

### Hash
```ruby
user = { name: 'aria', company: 'kakaomobility' } # {:name=>"aria", :company=>"kakaomobility"}
user[:name] # 'aria'
user[:phone] # nil
user.keys # [:name, :company]
user.to_a # [[:name, "aria"], [:company, "kakaomobility"]]
```
- iterate
```ruby
user = { name: 'aria', company: 'kakaomobility' }
user.each do |key, value|
  # do something
end
```

## Function
### function definition
- `def ... end`
- can have `?` at the end of the name of a function
- no return at the end
```ruby
def learning_ruby?
  true
end
```

- no `{`, `}`, sometimes do instead
```ruby
if satisfied
  do_something
else
  do_nothing
end
```
```ruby
while i < 10 do
	i += 1
end
```

## Class
```ruby
class User
  def initialize(name, company)
    @name    = name
    @company = company
  end
  
  def working?
    @company.present?
  end
end
```
- instantize 
```ruby
user = User.new('aria', 'kakaomobility')
user.working? # true
```

### Inheritance
```ruby
class VIP < User
  def initialize(name, company, phone)
    super(name, company)
    @phone = phone
  end
end
```

## Others
### Like letter
```ruby
send_push_message if user.agreed_to_receieve?
```

### Safe navigator
```java
user = User.get_by_name(‘아리아’)
if (user == null) {
  // do nothing
} else {
  user.sendPushMessage();
}
```
```ruby
user&.send_push_message
```
