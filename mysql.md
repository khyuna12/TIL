## pymysql 모듈

### **python이랑 연동하기**

1. 라이브러리 가져오기
  - `!pip install pymysql` -> MariaDB도 마찬가지
  - 오라클: `!pip install cx_Oracle`
  - `import pymysql`

2. 접속하기: `.connect()`로 MYSQL에 연결
  - 고속도로
  - `db = pymysql.connect(host, port, user, pw, db)`
    - `host`: 접속할 mysql server 주소
    - `port`: 접속할 mysql server 포트 번호
    - `user`: mysql ID
    - `passwd`: mysql ID의 암호
    - `db`: 접속할 데이터베이스
    - `charset=utf8`: mysql에서 select하여 데이터 가져올 때 한글이 깨질 수 있으므로 연결 설정에 넣어줌

3. 커서 가져오기: connect 객체로부터 `.cursor()` 메서드 호출하여 Cursor객체 가져옴
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
  