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
```sql
create table DEPARTMENT(
	id INT PRIMARY KEY,
	name VARCHAR(30) NOT NULL,
	birth_date DATE,
	sex CHAR(1) CHECK(sex in('M', 'F')),
	position VARCHAR(10),
	salary INT DEFAULT 5000000,
	dept_id INT,
	FOREIGN KEY(dept_id) references DEPARTMENT(id)
		on delete SET NULL on update CASCADE,
	CHECK(salary >= 50000000)
);

```


**PROJECT**

| <u>id</u> | name | leader_id | start_date | end_date |
| --------- | ---- | --------- | ---------- | -------- |
```sql
create table PROJECT(
	id INT PRIMARY KEY,
	name VARCHAR(20) NOT NULL UNIQUE,
	leader_id INT,
	start_date DATE,
	end_date DATE,
	FOREIGN KEY(leader_id) references EMPLOYEE(id)
		on delete SET NULL on update CASCADE
	CHECK(start_date < end_date)
)

```

**WORKS_ON**

| <u>empl_id | <u>proj_id |
| ---------- | ---------- |
``` sql
create table DEPARTMENT(
	empl_id INT,
	proj_id INT,
	PRIMARY KEY(empl_id, proj_id),
	FOREIGN KEY(empl_id) references EMPLOYEE(id)
		on delete CASCADE on update CASCADE,
	FOREIGN KEY(proj_id) references PROJECT(id)
		on delete CASCADE on update CASCADE
);
```

## attribute data type
###  숫자
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

### 문자
- 고정 크기 문자열
	- 최대 몇개의 '문자'를 가지는 문자열을 저장할지를 지정
	- 저장될 문자열의 길이가 최대 길이보다 작으면 나머지를 space로 채워서 저장
	- name char(4): 'a   ', '한국  ', '고고고고', 'wow '
	- CHAR(n) (0 <= n <= 255)
- 가변 크기 문자열
	- 최대 몇 개의 '문자'를 가지는 문자열을 저장할지를 지정
	- 저장될 문자열의 길이 만큼만 저장
	- name varchar(4): 'a', '한국', '고고고고', 'wow'
	- VARCHAR(n) (0 <= n <= 65,535)
- 사이즈가 큰 물자열
	- 사이즈가 큰 문자열을 저장할 때 사용
	- TINYTEXT, TEXT, MEDIUMTEXT, LONGTEXT

### 날짜와 시간
- 날짜
	- 년, 월, 일을 저장
	- YYY-MM-DD
	- DATE('1000-01-01' ~ '9999-12-31')
- 시간
	- 시, 분, 초를 저장
	- hh:mm:ss or hhh:mm:ss
	- TIME('-838:59:59' ~ '838:59:59')
- 날짜와 시간
	- 날짜와 시간을 같이 표현
	- YYY-MM-DD hh:mm:ss
	- TIMESTAMP는 time-zone이 반영됨(db의 타임존 기준)
	- DATETIME('1000-01-01 00:00:00' to '9999-12-31 23:59:59')
	- TIMESTAMP('1970-01-01 00:00:01' UTC ~ '2038-01-19 03:14:07' UTC)

### 그 외
- byte-string
	- byte string을 저장
	- BINARY, VARBINARY, BLOB type
- boolean
	- true, false를 저장
	- MySQL에는 따로 없음 => TINYINT롤 대체해서 사용
- 위치 관련
	- 위치 관련 정보를 저장
	- GEOMETRY
- JSON
	- json 형태의 데이터를 저장
	- JSON


##  Contraints

### PRIMARY KEY
- table의 tuple을 식별하기 위해 사용, 하나 이상의 attribute(s)로 구성
- primary key는 중복된 값을 가질 수 없으며, NULL도 값으로 가질 수 없다.

###  FOREIGN KEY
- attribute(s)가 다른 table의 **primary key**나 **unique key**를 참조할 때 사용
```sql
...
dept_id INT,
FOREIGN KEY(dept_id)
	references DEPARTMENT(id)
	on delete referce_option
	on update referce_option

```


| referce_option | 설명                          |
| -------------- | --------------------------- |
| CASCADE        | 참조값의 삭제/변경을 그래도 반영          |
| SET NULL       | 참조값이 삭제/변경 시 NULL로 변경       |
| RESTRICT       | 참조값이 삭제/변경되는 것을 금지          |
| NO ACTION      | RESTRICT와 유사                |
| SET DEFAULT    | 참조값이 삭제/변경 시 default 값으로 변경 |


### UNIQUE
- UNIQUE로 지정된 attribute(s)는 중복된 값을 가질 수 없다
- 단, NULL은 중복을 허용할 수도 있다(RDBMS 마다 다름)

### NOT NULL
- attribute가 NOT NULL로 지정되면 해당 attribute는 NULL을 값으로 가질 수 없다

### CHECK
- attribute의 값을 제한하고 싶은 때 사용

### attribute DEFAULT
- attribute의 default 값을 정의할 때 사용
- 새로운 tuple을 저장할 때 해당 attribute에 대한 값이 없다면 default 값으로 저장

### constraint 이름 명시하기
- 이름을 붙이면 어떤 constraint을 위반했는지 쉽게 파악 가능
- constraint를 삭제하고 싶을 때 해당 이름으로 삭제 가능
```sql
create table TEST(
	age INT CONSTRAINT age_over_20 CHECK(age > 20)
);
```
