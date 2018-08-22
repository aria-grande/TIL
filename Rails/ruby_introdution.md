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
- Local variable: variable shared in a block.
- Instance variable: variable shared among in an instance.
- Class variable: variable shared among all objects of a class.
```ruby
class User
  @@call_cnt = 0
  
  def initialize(name)
    @name = name
  end
	
  def call
    @@call_cnt += 1
  end
end

user1 = User.new('aria')
user1.call

User.class_variable_get(:@@called_cnt) # returns 1
user1.instance_variable_get(:@name) # 'aria'

user2 = User.new('lion')
user2.call

User.class_variable_get(:@@called_cnt) # returns 2
user2.instance_variable_get(:@name) # 'lion'
```

- Global variable: variable shared in anywhere in the program.
**Dangerous!!** Should be used sparingly.


### Substituting Variables into Strings
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

### Default argument
- can set default value when argument is `nil`.
```ruby
def calculate(income = 0, outcome = 0)
  income - outcome
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
### Instance method
A method only be called with an instance.

### Class method
A method called without an instance, not beubg tied to any particular object.
```ruby
class User
  # ...
	
  def User.find_by_name
    # ...
  end
end
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

### Access Control
Access levels to methods within class or module definitions using one or more these functions `public`, `protected`, `private`, like Java.

- public
callable with an instance.

- private
Both Private and Protected methods are not accessible from outside of the object as they are used internally to the object.
callable in an instance.

- protected
A Protected method is not accessible from outside of the context of the object, but it is **accessible from inside the context of another object of the same type.**

```ruby
class User
  def ==(other_user)
	  self.secret == other_user.secret
	end
	
  def encrypted_secret
    encrypt(self.secret)
  end
	
  protected
	
  def secret
    'secret key number'
  end
	
  private
	
  def secret_for_self
    self.secret
  end
end

user = User.new
user.secret # protected method 'secret' for #User:sdfd1 (No Method Error)
user.secret_for_self # private method 'secret_for_self' for #user:sdfd1 (No Method Error)
user.encrypted_secret # returns the content

user2 = User.new
user == user2
```

## Others
### Like letter
```ruby
send_push_message if user.agreed_to_receieve?
```

### Safe navigator
```java
user = User.getByName(‘아리아’)
if (user != null) {
  user.sendPushMessage();
}
```
```ruby
user&.send_push_message
```
