# 개요
Rails는 초기 구동 시 DB 스키마 캐싱을 하고 있기 때문에 DB 스키마 변경 시 이미 구동 중인 Rails 서버의 스키마와 DB 스키마가 불일치하는 현상이 발생할 수 있다.

Rails를 리스타트하면 변경된 DB 스키마 정보를 다시 긁어와서 캐싱하여 문제는 발생하지 않지만 리스타트하기 전까지는 unknown column error가 발생하거나 인덱스를 타지 않아 슬로우 쿼리가 발생한다.

업무 환경 상, production 환경에서는 DDL 권한이 없기에 배포시 migration을 하고 있지 않다.

번거롭더라도 zerodowntime migration을 위한 방법을 적어본다.


## 컬럼 추가
1. DB에 먼저 컬럼 추가(필요할 경우 새로운 컬럼에 대한 데이터 마이그레이션도 포함)

2. Rails 배포
```ruby
class AddNewColumnToModel < ActiveRecord::Migration[5.1]
  add_column :models, :new_column, :string
end
```

## 컬럼 삭제
DB에서 먼저 삭제하면 schema cache와 불일치 해서, `undefined method`, `unknown column` 에러 발생.

1. Rails 배포
캐싱된 스키마에는 `old_column`을 가지고 있을 것이기 때문에 DB에서 삭제하기 전까지 임시적으로 reject 처리.
```ruby
class User < ActiveRecord::Base
...
  # << REMOVE ON NEXT RELASE 
  def self.columns 
    super.reject{ |c| c.name.eql? "old_column" }
  end
  # << REMOVE ON NEXT RELASE 
...
end

```
2. DB에서 컬럼 삭제
3. 다음 Rails 배포 때, `reject` 지울 것!


## 컬럼 이름 변경
1. [컬럼 추가](#컬럼-추가)
2. [컬럼 삭제](#컬럼-삭제)


## 컬럼 타입 변경
인덱스가 걸려 있지 않은 컬럼이면서 변경하는 타입이 DBMS에서 자동으로 캐스팅 (예: int → string) 되는 경우는 별도의 작업을 하지 않아도 된다.<br/>
그 이외에는 변경하려는 타입으로 새로운 컬럼을 하나 더 생성하고 데이터 마이그레이션 및 배포 이후 기존 컬럼을 삭제.
1. [컬럼 추가](#컬럼-추가)
2. [컬럼 삭제](#컬럼-삭제)
 


## 인덱스 추가
기본적으로 인덱스를 추가하는 동안 table에 lock이 걸리며, 마이그레이션이 끝날 동안 create, update 쿼리를 수행할 수 없다.<br/>
1. DB에 인덱스 추가
2. 마이그레이션 코드 배포
```ruby
class AddIndexToUsersOnName < ActiveRecord::Migration
  disable_ddl_transaction!
  
  def change
    add_index :users, :name, algorithm: :concurrently
  end
end
```

## 인덱스 삭제
1. 마이그레이션 코드 배포
2. DB에서 인덱스 삭제


<hr/>
Refer: https://medium.com/klaxit-techblog/zero-downtime-migrations-with-activerecord-47528abe5136
