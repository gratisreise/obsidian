>SQL 뜻
- Structured Query Language
- 현업에서 쓰이는 relational DBMS의 표준 언어
- 종합적인 database 언어: DDL + DML + VDL

> SQL 주요 용어

| relational data model | sql    |
| --------------------- | ------ |
| relation              | table  |
| attribute             | column |
| tuple                 | row    |
| domain                | domain |

>SQL에서 relatin이란?
- multiset(= bag) of tuples @ SQL
- 중복된 tuple을 허용한다

> IT회사 관련 RDB 만들기
- 부서, 사원, 프로젝트 관련 정보들을 저장할 수 있는 관계형 데이터베이스를 만들자
- 사용할 RDBMS는 MySQL(InnoDB)

>My SQL 명령어

| 명령어                      | 설명                      |
| ------------------------ | ----------------------- |
| show databases           | 터미널에서 database 목록을 띄워준다 |
| create database company  | 새로운 데이터 베이스 생성          |
| select database()        | 선택된 데이터베이스 확인           |
| use {데이터베이스명}            | 데이터베이스 선택               |
| drop  database {데이터베이스명} |                         |

>DATABASE vs SCHEMA
- MySQL에서는 DATABASE와 SCHEMA가 같은 뜻을 의미
- create datebase {db이름} = create schema {db이름}
- 다른 RDBMS에서는 의미가 다르게 쓰임
- i.g PostgreSQL에서는 SCHEMA가 DATABASE의 namespace를 의미한다

### 관계형 DB 만들기

> IT 회사 RDB 만들기
- 부서, 사원, 프로젝트 관련 정보들을 저장할 수 있는 관계형 데이터 베이스


**DEPARTMENT**

| <u>id</u> | name | leader_id |
| --------- | ---- | --------- |
``` sql
create table DEPARTMENT(
	id INT PRIMARY KEY,
	name VARCHAR(20) NOT NULL UNIQUE,
	leader_id INT
);
```

**EMPLOYEE**

| <u>id</u> | name | birth_date | sex | position | salary | dept_id |
| --------- | ---- | ---------- | --- | -------- | ------ | ------- |


**PROJECT**

| <u>id</u> | name | leader_id | start_date | end_date |
| --------- | ---- | --------- | ---------- | -------- |

**WORKS_ON**

| <u>empl_id | <u>proj_id |
| ---------- | ---------- |

### attribute data type: 숫자
- 정수 : 정수를 저장할 때 사용
	- 1 byte: TINYINT
	- 2 byte: SMALLINT
	- 3 byte: MEDIUMINT
	- 4 byte: INT or INTEGER
	- 8 byte: BIGINT
- 부동 소수점 방식(floating-point): 실수(real number)를 저장, 고정 소수점에 비해 정확성이 떨어짐
	- 4 byte: FLOAT
	- 8 byte: DOUBLE or DOUBLE PRECISION
- 고정 소수점 방식(fixed-point): 실수를 정확하게 저장할 때 사용, DECIMAL(precision, scale)
	- ex) DECIMAL(5,2) =>[-999.99 ~ 999.99]
	- variable:  DECIMAL or NUMERIC



