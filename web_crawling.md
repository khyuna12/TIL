## Web crawling(웹 크롤링)과 scraping(스크레이핑)

> 크롤러: 자동으로 웹 페이지에 있는 정보를 수집하는 프로그램  
> 크롤링: 크롤러로 정보를 수집하는 것
>
> 스크레이핑: 수집한 정보를 분석해서 필요한 정보를 추출하는 것

<br>

### 크롤러의 처리 과정

1. 수집
  - 데이터 요청
2. 분석
  - 텍스트 데이터 -> 구조화 데이터
3. 추출
  - 구조화 데이터 추출
4. 가공
  - 가능한 데이터로 가공
5. 저장
  - 데이터베이스에 저장
  - SQL로 검색 가능


<br>

### 웹 브라우저 실행
- 기본 웹브라우저 자동 실행, 해당 url 주소로 접속
```python
import webbrowser
webbrowser.open("www.url.com")
```

<br>

### 웹 페이지 추출

- 표준 라이브러리 `urilib.request` 모듈 사용
- `urilib.request`의 `urlopen()`함수 이용
```python
from urllib.request import urlopen

 f = urlopen('http://url.co.kr')  # HTTPResponse 자료형의 객체 반환
```
```python
 type(f)
 f.read()  # read 메서드: HTTP 응답 본문(bytes 자료형) 추출
 f.status  # 상태 코드 추출
 f.getheader('Content-Type')  # HTTP 헤더의 값 추출
 ```

<br>

### 웹 페이지에서 데이터 추출
- **정규표현식**으로 스크레이핑
  - 표준 라이브러리의 re 모듈
```python
import re
from html import unescape
```

- **XML 스크레이핑**
  - 블로그 또는 뉴스 웹사이트 등의 웹사이트는 변경 정보 등을 RSS라는 이름의 XML 형식으로 제공
  - html보다 간단히 파싱
  - 내부에 피드를 나타내는 channel 요소가 있음

<br>

### 데이터 저장하기
- csv 형식으로 저장
- JSON 형식으로 저장
- 데이터베이스에 저장

<br>

---

<br>

### 웹 사이트에 접근시 / 수집한 데이터 다룰 때 주의 사항

- 웹 사이트 이용 규약 확인
- robots.txt와 robots 메타 태그의 접근 제한 사항 준수
- 상대 서버에 부하가 가지 않을 정도의 속도로 접근
- rel="nofollow"가 설정돼 있으면 접근 X
- 저작권 준수
- 수집한 데이터 기반 검색 서비스는 문제가 없을 때만 제공

<br>



