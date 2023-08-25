### DB(DataBase): 설계(1)
1. 모델링: 경력 필요한 경우 많음
2. 저장
3. 검색

<br>

#### DB/DBMS 특징

  - 데이터의 **무결성(Integrity)**
    - 데이터 오류 없어야 
    - **제약 조건(Constrain)**
      - *기본 키(Primary Key)*
        - 기본 키 열은 각 행을 구분하는 유일한 열
        - 중복X, nullX
        - 테이블마다 하나만
        - 자동으로 클러스터형 인덱스 생성: 내부적으로 컴퓨터가 key를 만듦 (예: 'KBS' -> 123457)
      - *외래 키(Foreign Key)*
        - 두 테이블의 관계 맺어주는 키
        - 하나의 테이블이 다른 테이블에 의존
        - 외래 키 테이블이 참조하는 기준 테이블의 열은 반드시 PK거나 Unique 제약 조건이 설정되어 있어야 함
        - 옵션: ON DELETE CASCADE, ON UPDATE CASCADE
        - 기준 테이블 데이터 변경되면 외래 키 테이블도 자동으로 적용
      - *UNIQUE*
        - 중복되지 않는 유일한 값
        - PK와 비슷, but NULL값 허용
        - NULL은 중복 가능
      - *CHECK*
        - 입력되는 데이터 점검
      - *DEFAULT*
        - 값 입력하지 않았을 때 자동으로 입력되는 기본 값 정의
      - *NULL 값 허용*
        - 허용: NULL
        - 허용 안 함: NOT NULL
        - 공백(` `)이나 0과 다름

  - 데이터의 **독립성**
    - 데이터베이스 크기 변경하거나 데이터 파일의 저장소 변경 시 기존에 작성된
    응용프로그램은 전혀 영향을 받지 않음

  - 보안
    - 데이터에 접근이 허가된 사람만 접근 가능
    - 사용자의 계정에 따라 다른 권한

  - 데이터 중복의 최소화

  - 응용프로그램 제작 및 수정이 쉬워짐

  - 데이터의 안정성 향상
    - DBMS가 제공하는 백업, 복원 기능 이용

---

### SQL: 처리(2)
1. DDL: table, DB 생성, 삭제, 수정
2. DML: select, update
3. DCL: delete, insert, 권한

---

### 운영: 관리(3)
1. 보안
2. 백업(장애 대응)

<br>

---

<br>

---

<br>

### File System

- File
- Dir
  - txt, csv

- 중복

---

### DBMS(DataBase Management System)

- 파일 시스템의 단점 보완
- 데이터의 집합인 데이터베이스를 잘 관리하고 운영하기 위한 시스템/소프트웨어


#### RDBMS(table)

- Oracle: 관리비 많이 듦, 잘 안 쓰는 추세
- MySQL
- MSSQL
- SYBASE
- DB2
- SQLite

<br>

---

<br>

### 정보시스템 구축 절차
> 분석 - 설계 - 구현 - 시험 - 유지보수

<br>

- **분석**
  - 시스템 분석 또는 요구사항 분석
  - 요구사항 분석: 현재 우리가 무엇(What)을 할 것인지 결정
  - 사용자의 인터뷰와 업무 조사 등 수행
  - 분석의 결과로 문서 작성

<br>

- **설계**
  - 시스템 설계 또는 프로그램 설계
  - 구축하고자 하는 시스템을 어떻게(How) 할 것인지 결정
  - **분석과 설계의 과정이 전체 프로젝트의 50% 이상** 차지

<br>

- **모델링**
  - 현실에 사용되는 데이터를 MYSQL에 어떻게 옮겨 놓을 것인지 결정
  - 테이블(Table) 형식에 맞춰 저장
    

<br>

- **데이터베이스 구축/관리 및 활용** 
  - DBMS 설치
  
  - 데이터베이스 구축 절차
    - 데이터베이스 생성: `create DataBase`
    - 테이블 생성: `create table`
    - **데이터 입력(모델링 끝나고)**
    - **데이터 조회/활용**

  - 테이블 외의 데이터베이스 개체의 활용: DB 모델링
    - 데이터 백업 및 관리

  - 응용 프로그램에서 구축된 데이터 활용(웹 서비스/애플리케이션)

<br>

- **데이터 활용**
  - SELECT문

  - 뷰(View)
    - 가상의 테이블
    - 저장할 필요 X(저장 공간 확보)
    - 필요한 것만 보여줌

  - 스토어드 프로시저(Stored Procedure)
    - SQL문을 하나로 묶어 편리하게 사용
    - 다른 프로그래밍 언어와 같은 기능을 담당할 수도 있음

  - 트리거(Trigger)
    - 테이블에 부착되어 테이블에 INSERT, UPDATE, DELETE 작업이 발생되면 실행되는 코드

  - 백업
    - 현재의 데이터베이스를 다른 매체에 보관하는 작업
  
  - 복원
    - 데이터에베이스에 문제 발생 시 다른 매체에 백업된 데이터를 이용해 원상태로 돌려놓는 작업
    - 백업과 복원은 DBA(데이터베이스 관리자)가 해야 할 가장 중요한 일

<br>

---

<br>

### SQL(Structured Query Language)

- DBMS에 데이터 구축/관리/활용 위해서 사용되는 언어
- DBMS 통해 중요한 정보들 입력, 관리, 추출
- DBMS 제작 회사와 독립적
- 분산형 클라이언트/서버 구조
- 대화식 언어

#### NoSQL(JSON)

- MongoDB
- HBASE(하둡)
- `{key: value}`

<br>

#### SQL 기본

- **USE문**
  - SELECT문 학습 위해 사용할 데이터베이스 지정
  - 이후 모든 SQL문은 지정 DB에서 수행
```sql
USE 데이터베이스_이름;
```

- **SELECT문**
```sql
SELECT * FROM 데이터베이스_이름;
```

- DB, TABLE, 열 조회

```sql
-- 현재 서버에 어떤 DB 있는지
SHOW DATABASES;
```

```sql
-- 현재 서버에 어떤 TABLE 있는지
SHOW TABLE STATUS; 
SHOW TABLES;
```

```sql
-- 열
DESCRIBE 데이터베이스_이름;
DESC 데이터베이스_이름;
```

 - **데이터베이스 만들기**
  - SCHEMAS 마우스 오른쪽 클릭 > create Schemas ...

  - 코드로 만들기
  ```sql
  CREATE DATABASE tabledb;
  ```

- **테이블 만들기** + 제약조건
```sql
use tabledb;
drop table if exists buytbl, usertbl;

CREATE TABLE buytbl 
(  num INT AUTO_INCREMENT NOT NULL PRIMARY KEY, 
   userid  CHAR(8) NOT NULL ,
   prodName CHAR(6) NOT NULL,
   groupName CHAR(4) NULL , 
   price     INT  NOT NULL,
   amount    SMALLINT  NOT NULL 
);


DROP TABLE IF EXISTS buytbl;
CREATE TABLE buytbl 
(  num INT AUTO_INCREMENT NOT NULL PRIMARY KEY, 
   userid  CHAR(8) NOT NULL ,
   prodName CHAR(6) NOT NULL,
   groupName CHAR(4) NULL , 
   price     INT  NOT NULL,
   amount    SMALLINT  NOT NULL 
   , FOREIGN KEY(userid) REFERENCES usertbl(userID)
);
```

- **python이랑 연동하기**

1. 라이브러리 가져오기
  - `!pip install pymysql` -> MariaDB도 마찬가지
  - 오라클: `!pip install cx_Oracle`
  - `import pymysql`

2. 접속하기
  - 고속도로
  - `db = pymysql.connect(host, port, user, pw, db)`
    - `host`: 접속할 mysql server 주소
    - `port`: 접속할 mysql server 포트 번호
    - `user`: mysql ID
    - `passwd`: mysql ID의 암호
    - `db`: 접속할 데이터베이스
    - `charset=utf8`: mysql에서 select하여 데이터 가져올 때 한글이 깨질 수 있으므로 연결 설정에 넣어줌

3. 커서 가져오기
  - 데이터 전용도로
  - `cursor = db.cursor()`: cursor Object 가져오기

4. SQL문 작성하기(CRUD SQL 구문 작성)
  - `select`, `update`, `delete`, `insert`
  - `sql = select * from table`

5. SQL문 실행하기
  - `cursor.execute(sql)`
  
  - `result = cursor.fetchall()`: 데이터베이스 전부 보여줌
  - `cursor.fetchone()`
  - `cursor.fetchmany()`

6. DB commit하기(실행 mysql 서버에 확정 반영)
  - `select`할 때는 상관없음
  - `update`, `delete`, `insert` 데이터가 변경/추가 할 때 커밋 필수
  - `db.commit()`: 안 하면 선배들한테 혼남(락 오랫동안 -> 데드락 -> 시스템 다운됨)

7. DB 연결 닫기
  - `close()`
  - 안 닫으면 서버 부하 올 수도 있음

- 연결 - close: `with`랑 비슷
  