# Self-referencing Relationship

## What?
일반적으로 우리가 관계를 맺는 것은 테이블 간의 reference다.<br/>
특이하게도, self-referencing은 테이블 내의 records 사이의 관계를 표현한 것으로, _recursive_ relationship 이라고도 불린다.<br/>
dual-table relationship 처럼 one-to-one, one-to-many, many-to-many 관계가 생성 될 수 있다.

### One-to-One
_self-referencing one-to-one_ 관계는 테이블 내 주어진 record가 테이블 내의 only one 다른 record와 관련이 맺을 때 사용된다.

#### Members
아래 테이블은 member들의 정보를 담고 있으며, 한 멤버는 only one 다른 멤버를 스폰싱 할 수 있다.

|ID  | Name | Sponser ID| other fields |
|----|------|-----------|:------------:|
|1001|Aria  |           |       ...    |
|1002|Joe   | 1001      |       ...    |
|1003|Tom   | 1002      |       ...    |
|1004|Donna |           |       ...    |

### One-to-Many
_self-referencing one-to-many_ 관계는 테이블 내 주어진 record가 테이블 내 하나 이상의 records와 관계를 맺을 때 사용한다.<br>

#### Members
아래 테이블은 member들의 정보를 담고 있으며, 한 멤버는 다른 멤버들의 스폰서가 될 수 있다.

|ID  | Name | Sponser ID| other fields |
|----|------|-----------|:------------:|
|1001|Aria  |           |       ...    |
|1002|Joe   | 1001      |       ...    |
|1003|Tom   | 1002      |       ...    |
|1004|Donna | 1002      |       ...    |


### Many-to-Many
_self-referencing many-to-many_ 관계는 테이블 내 주어진 하나 이상의 records가 테이블 내 하나 이상의 records와 관계를 맺을 때 사용한다.<br/>

#### User
|ID | Name | Friend ID | other fields|
|----|------|----------|:------------:|
|1001|Aria  | 1002     |       ...    |
|1002|Joe   | 1001     |       ...    |
|1003|Tom   | 1004     |       ...    |
|1004|Donna | 1003     |       ...    |

## So, Bad or good?
안티 디자인 패턴은 아니다.

## Reference
- [Database Design for Mere Mortals](https://books.google.co.kr/books?id=dkxsjXNayHQC&pg=PA338&lpg=PA338&dq=database+self+reference&source=bl&ots=eV51hVZ9F_&sig=xC2Nk0IFO8Mqh60f6M94FKIEKKA&hl=ko&sa=X&ved=2ahUKEwjhvv3hmL_cAhWFzmEKHQfYBQYQ6AEwC3oECAcQAQ#v=onepage&q=self%20reference&f=false)
