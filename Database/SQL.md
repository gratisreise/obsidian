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


### ALTER TABLE
- table의 Schema를 변경하고 싶을 때 사용
- 이미 서비스 중인 table의 schema를 변경하는 것은 신중하게 하자

| 유형              | 예제                                                     |
| --------------- | ------------------------------------------------------ |
| attribute 추가    | ALTER TABLE employee ADD blood VARCHAR(2);             |
| attribute 이름 변경 | ALTER TABLE employee RENAME COLUMN phone TO phone_num; |
| attribute 타입 변경 | ALTER TABLE employee MODIFY COLUMN blood CHAR(2);      |
| table 이름 변경     | ALTER TABLE logs RENAME TO backend_logs;               |
| ...             | ...                                                    |

## database 구조를 정의할 때 중요한 점
만들려는 서비스의 스펙과 **데이터 일관성**, **편의성**, **확장성** 등등을 종합적으로 고려하여 DB 스키마를 적절하게 정의하는 것이 중요하다 


### SELECT를 사용할 때 주의할 점
1. SELECT로 조회할 때 조건들을 포함해서 조회를 한다면 이 조건들과 관련된 attributes에 index가 걸려있어야 한다. 그렇지 않다면 데이터가 많아질수록 조회 속도가 느려진다
2. 현재 mysql 기준이기 때문에 다른 RDB 사용시 참고해서 사용해라


## subquery

- **subquery**는 SELECT, INSERT, UPDATE, DELETE에 포함된 query
- **outer query**(main query)는 subquery를 포함하는 query
- **subquery**는 () 안에 기술된다
- v IN (v1, v2, v3,...):v가 (v1, v2, v3...)중에 하나와 값이 같다면 TRUE를 return 한다
- (v1, v2, v3,...)는 명시적인 값들의 집합일 수도 있고 subquery의 결과(set or multiset)일 수도 있다
- v NOT IN(v1, v2, v3,...) : v가 () 안의 모든 값과 값이 다르다면 TRUE를 return 한다
- unqualified attribute가 참조하는 table은 해당 attribute가 사용된 query를 포함하여 그 query의 바깥쪽으로 존재하는 모든 queries 중에 해당 attribute 이름을 가지는 가장 가까이에 있는 table을 참조한다

```sql
%% ID가 5인 임직원과 같은 프로젝트에 참여한 임직원들의 ID와 이름을 알고 싶다 %%
SELECT id, name FROM employee
WHERE id IN(
	SELECT DISTINCT empl_id
	FROM works_on
	WHERE empl_id != 5 AND proj_id IN(
			SELECT proj_id
			FROM workd_on
			WHERE empl_id = 5
	)
)

SELECT id, name FROM employee, (
	SELECT DISTINCT empl_id
	FROM works_on
	WHERE empl_id != 5 AND proj_id IN(
			SELECT proj_id
			FROM workd_on
			WHERE empl_id = 5
	) AS DISTINCT_E
WHERE id = DISTINCT_E.empl_id

```

```sql
SELECT P.id, P.name
FROM project P
WHERE EXISTS(
		SELECT * FROM works_on W
		WHERE W.proj_id = P.id AND W.empl_id IN(7, 12)
)
```
- correlated query: subquery가 바깥쪽 query의 attribute를 참조할 때, correlated subquery라 부름
- EXISTS: subquery의 결과가 최소 하나의 row라도 있다면 TRUE를 반환
- NOT EXISTS: subquery의 결과가 단 하나의 row도 없다면 TRUE를 반환


```sql
SELECT E.id, E.name, E.salary, (
		SELECT max(salary) FROM employee
		WHERE dept_id = E.dept_id
	) AS dept_max_salary
FROM department D, employee E
WHERE D.leader_id = E.id AND E.salary < ANY(
		SELECT salary
		FROM employee
		WHERE id != D.leader_id AND dept_id = E.dept_id
	);

```
- v comparison_operator **ANY**(subquery): subquery가 반환한 결과들 중에 단 하나라도 v와의 비교 연산이 TRUE라면 TRUE를 반환한다
- **SOME**도 **ANY**와 같은 역할을 한다

```sql
SELECT DISTINCT E.id, E.name, E.position
FROM employee E, works_on W
WHERE E.id = W.empl_id AND W.proj_id != ALL(
		SELECT proj_id
		FROM works_on
		WHERE empl_id = 13
	);

```

1. 성능 비교 : IN vs EXISTS => 최근 성능차이가 거의없다




## JOIN

- 두 개 이상의 table들에 있는 데이터를 한 번에 조회하는 것
- 여러 종류의 JOIN이 존재한다
- implicit join
- explicit join

### implicit join
`from절에는 table들만 나열하고 where절에 join condition을 명시하는 방식 `

```SQL
%% example code %%
SELECT D.name
FROM employee AS E, department AS D
WHERE E.id = 1 and E.dept_id = D.id;
```


- old-style join syntax
- where절에 selection condition과 join condition이 같이 있기 때문에 **가독성**이 떨어진다
- 복잡한 join 쿼리를 작성하다 보면 실수롤 잘못된 쿼리를 작성할 가능성이 크다

### explicit join
`from절에 JOIN 키워드와 함께 joined table들을 명시하는 방식`
```SQL
%% example code %%
SELECT D.name
FROM employee AS E JOIN department AS D ON E.dept_id = D.id
WHERE E.id = 1
```
- from절에서 ON 뒤에 join condition이 명시된다
- 가독성이 좋다
- 복잡한 join 쿼리 작성 중에도 실수할 가능성이 작다

### inner join
`두 table에서 join condition을 만족하는 tuple들로 result table을 만드는 join`
```SQL
SELECT *
FROM employee E INNER JOIN department D ON E.dept_id = D.id;
```
- FROM table1 [inner]JOIN table2 ON join_condition
- join condition에 사용 가능한 연산자(operator) : = , <, >, != 등등 여러 비교 연산자가 가능하다
- join condition에서 null 값을 가지는 tuple은 result table에 포함되지 못한다

### outer join
`두 table에서 join condition을 만족하지 않는 tuple들도 result table에 포함하는 join`
```SQL
SELECT *
%% FROM employee E LEFT OUTER JOIN department D ON E.dept_id = D.id; %%
%% FROM employee E RIGHT OUTER JOIN department D ON E.dept_id = D.id; %%
%% FROM employee E FULL OUTER JOIN department D ON E.dept_id = D.id; %%
```
- FROM table1 LEFT [OUTER] JOIN table2 ON join_condition
- FROM table1 RIGHT [OUTER] JOIN table2 ON join_condition
- FROM table1 FULL [OUTER] JOIN table2 ON join_condition
- join condition에 사용 가능한 연산자(operator): =, <, >, != 등등 여러 비교 연산자가 가능하다

### equi join
- join condition에서 = (equality comparator)를 사용하는 join

### equi join에 대한 두 가지 시각
- inner join outer join 상관없이 = 를 사용한 join이라면 equi join으로 보는 경우
- inner join으로 한정해서 = 를 사용한 경우에 equi join으로 보는 경우

### USING
```SQL
SELECT D.name
FROM employee E JOIN department D USING(dept_id);
```
- 두 table이 equi join할 때 join하는 attribute의 이름이 같다면, USING으로 간단하게 작성할 수 있다
- 이 때 같은 이름의 attribute는 result table에서 한번만 표시 된다
- FROM table1 [INNER] JOIN table2 USING (attribute(s))
- FROM table1 LEFT [OUTER] JOIN table2 USING (attribute(s))
- FROM table1 RIGHT [OUTER] JOIN table2 USING (attribute(s))
- FROM table1 FULL [OUTER] JOIN table2 USING (attribute(s))

### natural join
```SQL
SELECT D.name
FROM employee E NATURAL INNER JOIN department D;
```
- 두 table에서 같은 이름을 가지는 모든 attribute pair에 대해서 equi join을 수행
- join condition을 따로 명시하지 않는다
- FROM table1 NATURAL [INNER] JOIN table2
- FROM table1 NATURAL LEFT [OUTER] JOIN table2
- FROM table1 NATURAL RIGHT [OUTER] JOIN table2
- FROM table1 NATURAL FULL [OUTER] JOIN table2

### cross join

- 두 table의 tuple pair로 만들 수 있는 모든 조합(= Cartesian product)을 result table로 반환한다
- join condition이 없다
- implicit cross join: FROM table1, table2
- explicit cross join: FROM table1 CROSS JOIN table2
@ MySQL
- MySQL에서는 cross join = inner join = join 이다
- CROSS JOIN에 ON(or USING)을 같이 쓰면 inner join으로 동작한다
- INNER JOIN(or JOIN)이 ON(or USING)이 없이 사용되면 cross join으로 동작한다

### self jion
- table이 자기 자신에게 join하는 경우

### join example
- ID가 1003인 부서에 속하는 임직원 중 리더를 제외한 부서원의 ID, 이름, 연봉을 알고 싶다
```MySQL
SELECT E.id, E.name, E.salary
FROM employee E JOIN department D ON E.dept_id = D.id
WHERE E.dept_id = 1003 and E.id != D.leader_id;
```

- ID가 2001인 프로젝트에 참여한 임직원들의 이름과 직군과 소속 부서 이름을 알고 싶다
```MySQL
SELECT E.name AS empl_name, E.position AS empl_position, D.name AS dept_name
FROM works_on W JOIN employee E ON W.empl_id = E.id
				LEFT JOIN department D ON E.dept_id = D.id
WHERE W.proj_id = 2001;
```

### ORDER BY
```MYSQL
SELECT * FROM employee ORDER BY salary;
```
- 조회 결과를 특정 attribute(s) 기준으로 정렬하여 가져오고 싶을 때 사용한다
- default 정렬 방식은 오름차순이다
- 오름차순 정렬은 ASC로 표기한다
- 내림차순 정렬은 DESC로 표기한다

### aggregate function
```MySQL
SELECT COUNT(*) FROM employee;

%% 프로젝트 2002에 참여한 임직원 수와 최대 연봉과 최소 연봉과 평균 연봉을 알고싶다 %%
SELECT COUNT(*), MAX(salary), MIN(salary), AVG(salary)
FROM works_on W JOIN employee E ON W.empl_id = E.id
WHERE W.proj_id = 2002;

```
- 여러 tuple들의 정보를 요약해서 하나의 값으로 추출하는 함수
- 대표적으로 COUNT, SUM, MAX, MIN, AVG 함수가 있다
- (주로) 관심있는 attribute에 사용된다 e.g) AVG(salary), MAX(birth_date)
- NULL 값들은 제외하고 요약 값을 추출한다

### GROUP BY
``` MySQL
%% 각 프로젝트에 참여한 임직원 수와 최대 연봉과 최소 연봉과 평균 연봉을 알고 싶다 %%
SELECT W.proj_id, COUNT(*), MAX(salary), MIN(salary), AVG(salary)
FROM works_on W JOIN employee E ON W.empl_id = E.id
GROUP BY W.proj_id;
```
- 관심있는 attribute(s) 기준으로 그룹을 나눠서 그룹별로 aggregate function을 적용하고 싶을 때 사용
- grouping attribute(s): 그룹을 나누는 기준이 되는 attribute(s)
- grouping attribute(s)에 NULL 값이 있을 때는 NULL 값을 가지는 tuple끼리 묶인다

### HAVING
```MySQL
%% 참여인원이 7명 이상인 프로젝트 임직원 수와 최대 연봉과 최소 연봉과 평균 연봉을 알고 싶다 %%
SELECT W.proj_id, COUNT(*), MAX(salary), MIN(salary), AVG(salary)
FROM works_on W JOIN employee E ON W.empl_id = E.id
GROUP BY W.proj_id
HAVING COUNT(*) >= 7;


```
- GROUP BY와 함께 사용한다
- aggregate function의 결과값을 바탕으로 그룹을 필터링하고 싶을 때 사용한다
- HAVING절에 명시된 조건을 만족하는 그룹만 결과에 포함된다

### Example
```MySQL
%% 각 부서별 인원수를 인원 수가 많은 순서대로 정렬해서 알고 싶다 %%
SELECT dept_id, COUNT(*) AS empl_count 
FROM employee
GROUP BY dept_id,
ORDER BY empl_count DESC;

%% 각 부서별 인원수를 인원 수가 많은 순서대로 정렬해서 알고 싶다 %%
SELECT dept_id,sex, COUNT(*) AS empl_count 
FROM employee
GROUP BY dept_id, sex
ORDER BY empl_count DESC;

%% 회사 전체 평균 연봉보다 평균 연봉이 적은 부서들의 평균 연봉을 알고 싶다 %%
SELECT dept_id, AVG(salary)
FROM employee
GROUP BY dept_id
HAVING AVG(salary) <(
	SELECT AVG(salary) FROM employee
);

%% 각 프로젝트별로 프로젝트에 참여한 90년대생들의 수와 이들의 평균 연봉을 알고 싶다 %%
SELECT proj_id, COUNT(*), ROUND(AVG(salary), 0)
FROM works_on W JOIN employee E ON w.empl_id = E.id
WHERE E.birth_date BETWEEN '1990-01-01' AND '1999-12-31'
GROUP BY W.proj_id;

%% 각 참여인원이 7명 이상인 프로젝트 중 참여한 90년대생들의 수와 이들의 평균 연봉을 알고 싶다 %%
SELECT proj_id, COUNT(*), ROUND(AVG(salary), 0)
FROM works_on W JOIN employee E ON w.empl_id = E.id
WHERE E.birth_date BETWEEN '1990-01-01' AND '1999-12-31'
	AND W.proj_id IN(SELECT proj_id FROM works_on
					 GROUP BY proj_id HAVING COUNT(*) >= 7)
GROUP BY W.proj_id;
ORDER BY W.proj_id;
```

### SELECT 요약
6. SELECT attribute(s) or aggregate function(s) 
1. FROM table(s) 
2. [WHERE condition(s)]
3. [GROUP BY group attributes(s)]
4. [HAVING group condition(s)]
5. [ORDER BY attribute(s)]
- select 쿼링에서 각 절(phrase)의 실행 순서는 개념적인 순서이다
- select 쿼리의 실제 실행 순서는 각 RDBMS에서 어떻게 구현했는지에 따라 다르다


