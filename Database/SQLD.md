
### 데이터베이스 설계순서
1. 요구 조건 분석: 요구 조건 명세서 작성
2. 개념적 설계: 개념 스키마, 트랜잭션 모델링, E-R 모델
3. 논리적 설계: 목표 DBMS에 맞는 논리 스키마 설계, 트랜잭션 인터페이스 설계
4. 물리적 설계: 목표 DBMS에 맞는 물리적 구조의 데이터로 변환
5. 구현: 목표 DBMS의 DDL(데이터 정의어)로 데이터베이스 생성, 트랜잭션 작성

### 개념적 설계(정보 모델링, 개념화)
현실 세계의 요소를 데이터베이스에 정리하기 위해 적절한 개념으로 설계하는 과정
- 개념 스키마 모델링과 트랜잭션 모델링을 병행 수행한다
- 요구 조건 명세서를 참고하여 E-R 다이어그램 작성
- DBMS에 독립적인 개념 스키마를 설계한다

### 논리적 설계(데이터 모델링)
현실세계의 자료를 DBMS에 지원하는 자료 구조로 변환(mapping)시키는 과정
- 논리적인 데이터 모델 설계
- 선택한 DBMS에 따른 논리적 스키마 설계
- 트랜잭션의 인터페이스를 설계
- 관계형이면 테이블을 설계

### 물리적 설계(데이터 구조화)
논리적 구조로 표현된 데이터를 디스크 등의 물리적 저장장치에 저장할 수 있는 물리적 구조의 데이터로 변환하는 과정
- 데이터베이스 파일의 저장 구조 및 액세스 경로를 결정한다.
- 저장 레코드의 양식, 순서, 접근 경로등의 정보를 사용하여 컴퓨터에 저장되는 방법을 묘사한다
- 고려사항: 트랜잭션 처리량, 응답 시간, 디스크 용량, 저장 공간의 효율화

### 데이터 모델
현실 세계의 정보들을 컴퓨터에 표현하기 위해서 단순화, 추상화하여 체계적으로 표현한 개념적 모형

| 개체(Entity)        | 데이터베이스에 표현하려는 것으로, 사람이 생각하는 개념이나 정보 단위      |
| ----------------- | ------------------------------------------- |
| 속성(Attribute)     | 데이터의 가장 작은 논리적 단위, 파일 구조상의 데이터 항목 or 데이터 필드 |
| 관계(Relationship)  | 객체 간의 관계 또는 속성 간의 논리적인 연결                   |
| 구조(Structure)     | 논리적으로 표현된 개체 타입들 간의 관계, 데이터 구조 및 정적 성질 표현   |
| 연산(Operation)     | 데이터베이스를 조작하는 기본 도구                          |
| 제약 조건(Constraint) | 논리적인 제약 조건                                  |

### E-R 모델의 개요
E-R 모델은 개념적 데이터 모델의 가장 대표적인 것으로, 1976년 피터 첸(Peter Chen)이 정립
- 개체 타입(Entity Type)과 이들 간의 관계 타입(Relationship Type)을 이용해 현실세계를 개념적으로 표현
- 데이터를 개체(Entity), 관계(Relationship), 속성(Attribute)으로 묘사한다
- DBMS를 고려하지 않는다
- 1:1, 1:N, N:M 등의 관계 유형을 제한 없이 나타낼 수 있다.

### E-R 다이어그램

| 기호 이름 | 의미                                    |
| ----- | ------------------------------------- |
| 사각형   | 개체(Entity) 타입                         |
| 마름모   | 관계(Relationship) 타입                   |
| 타원    | 속성(Attribute)                         |
| 이중 타원 | 다중값 속성(복합 속성)                         |
| 밑줄 타원 | 기본키 속성                                |
| 복수 타원 | 복합 속성                                 |
| 관계    | 1:1, 1:N, N:M 등의 개체 간 관계 대응수를 선 위에 기술 |
| 선, 링크 | 개체 타입과 속성을 연결                         |

### 관계형 데이터 모델





