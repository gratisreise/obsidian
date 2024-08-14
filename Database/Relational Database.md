
> set
- 서로 다른 elements를 가지는 collection
- 하나의 set에서 elements의 순서는 중요하지 않다
- ex) {1, 3, 11, 4, 7}

> relation in mathematics
- subset of Cartesian product
- set of tuples

> relation data model
- student relation을 예를 들어 relational data model을 이해해 보겠습니다

| 주요개념          | 설명                                          |
| ------------- | ------------------------------------------- |
| domain        | set of atomic values                        |
| domain name   | domain 이름                                   |
| attribute     | domain이 relation에서 맡은 역할 이름                 |
| tuple         | 각 attribute의 값으로 이루어진 리스트, 일부 값은 NULL일 수 있다 |
| relation      | set of tuples                               |
| relation name | relation의 이름                                |

> relation schema
- relation의 구조를 나타낸다
- relation 이름과 attributes 리스트로 표기된다
- e.g STUDENT(id, name, grade, major, phone_num)
- attributes와 관련된 constraints도 포함한다

> degree of a relation
- relation schema에서 attributes의 수
- e.g STUDENT(id, name, grade, major, phone_num) -> degree 6

>relational database
- relational data model에 기반하여 구조화된 database
- relational database는 여러 개의 relations로 구성된다

> realtion의 특징들
- relation의 중복된 tuple을 가질 수 없다(relation is set of tuples)
- relation의 tuple을 식별하기 위해 attribute의 부분 집합을 key로 설정한다
- relation에서 tuple의 순서는 중요하지 않다
- 하나의 relation에서 attribute의 이름은 중복되면 안된다.
- 하나의 relation에서 attribute의 이름은 순서는 상관없다.
- attribute는 atomic 해야 한다(composite or multivalued attribute 허용 안됨)

>NULL의 의미
- 값이 존재하지 않는다
- 값이 존재하난 아직 그 값이 무엇인지 알지 못한다
- 해당 사항과 관련이 없다