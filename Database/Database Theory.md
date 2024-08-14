
> Database

전자적으로(electronically, 컴퓨터에 저장 및 사용) 저장되고 사용되는 관련련있는(같은 출처 및 자연스럽게 생서되는) 데이터들의 조직화된 집합(체계적이게 잘 정리된 집합)

**데이터의 관리를 위해 체계화하여 저장하는 공간** 

> DBMS(DataBase Management Systems)

사용자에게 DB를 정의하고 만들고 관리하는 기능을 제공하는 소프트웨어 시스템
DB를 정의하다 보면 부가적인 데이터가 발생 -> metadata
ex) PostgreSQL, MySQL, ORACLE, MS-SQL

> metadata

데이터를 설명하기위한 데이터(data about data)

- database를 정의하거나 기술하는(descriptive) data, catalog라고도 부른다
- 예시: 데이터 유형, 구조, 제약 조건, 보안, 저장, 인덱스, 사용자 그룹 등등
- metadta 또한 DBMS를 통해 저장/관리된다.


> database system

- database + DBMS + 연관된 applications
- 줄여서 database라고도 부름(문맥에 따라 파악 필요)

![이미지](https://www.researchgate.net/publication/326006960/figure/fig1/AS:641949367279620@1530064064883/Simplified-database-system-Risunok-1-Uprosennaa-sistema-baz-dannyh-Slika.png)


> data models

- DB의 구조(structure)를 기술하는데 사용될 수 있는 개념들이 모인 집합
- DB 구조를 추상화(인간 친화적)해서 표현할 수 있는 수단을 제공한다
- data model은 여러 종류가 있으며 추상화 수준과 DB 구조화 방식이 조금씩 다르다
- DB에서 읽고 쓰기 위한 기본적인 동작들(operations)도 포함한다.
DB 구조: 데이터 유형, 데이터관계(relationship), 제약사항(constraints) 등등


> data models 분류

- conceptual(or high-level) data models
- logical(or representational) data models
- physical(or low-level) data models


> conceptual data models

- 일반 사용자들이 쉽게 이해할 수 있는 개념들로 이뤄진 모델
- 추상화 수준이 가장 높음
- 비즈니스 요구 사항을 추상화하여 기술할 때 사용


> logical data models

- 이해하기 어렵지 않으면서도 디테일하게 DB를 구조화 할 수 있는 개념들을 제공
- 데이터가 컴퓨터에 저당될 때의 구조와 크게 다르지 않게 DB 구조화를 가능하게 함
- 특정 DBMS나 storage에 종속되지 않는 수준에서 DB를 구조화할 수 있는 모델

ex) relational data model, object data model, object-relational data model


> physical data models

- 컴퓨터에 데이터가 어떻게 파일 형태로 저장되는지를 기술할 수 있는 수단을 제공
- data format, data orderings, access path등등
- access path: 데이터 검색을 빠르게 하기 위한 구조체 -> index

> database schema

- data model을 바탕으로 database의 구조를 기술(description)한 것
- schema는 database를 설계할 때 정해지며 한 번 정해진 후에는 자주 바뀌지 않는다


> database state
- database에 있는 실제 데이터는 꽤 자주 바뀔 수 있다.
- 특정 시점에 database에 있는 데이터를 database state 혹은 snapshot이라고 한다
- 혹은 database에 있는 현재 instances의 집합이라고 한다.

> three-schema architecture
- database system을 구축하는 architecture 중의 하나
- user application으로 부터 물리적인(physical) database를 분리시키는 목적
- 세 가지 level이 존재하며 각각의 level마다 schema가 정의되어 있다

3가지Level
- external
- conceptual
- internal



> Database Language


