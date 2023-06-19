## Web Application Architecture

<br>

1. client가 URL 입력 요청
2. server가 a.html 검색 - not Found 404 에러코드 여기서 반환(200 성공)
3. a.html 전달(응답) - 실행되는건 client에서
4. a. html 저장
5. 렌더링

<br>

URL 포맷:
```
http://서버ip:port번호/a.html
```

<br>

### 웹 서버

- Apache Ngix, Live Server, ...
- 정적 파일 처리(html, CSS, JS)

<br>

### Container

- python: Django(*.py)
- Java: jsp/servlet(*.java)
- MS: C#(*.asp)

<br>

---

<br>

## HTML

<br>

- DOM(Document Object Model)
  - html문서에 있는 tag에 해당되는 객체를 생성하고 tree로 만드는 구조
  - node
    - element node
    - attribute node
    - text node

- Query String
   - `key(name)=value` 형식
   - 다중 query string: `key=value&key=value`

```html
<form action="target.html">
		이름 <input type="text" name="username"><br>
		<input type="submit" value="전송">
</form>
```

```
http://서버ip:port번호/target.html?username=홍길동
```

- 경로 지정(중요)
  - 파일 또는 target 지정시 사용
  ```html
  <a href="경로">
  <form action="경로">
  <script src="경로">
  <link href="경로">
  <img src="경로">
  ```
  - 종류 2가지
    - 상대경로: 현재파일이 있는 디렉토리 기준
    - 절대경로: 최상위 디렉토리가 포함된 경로, '/'로 시작 


<br>

---

<br>

## CSS

<br>

- 스타일 지정
- html에서 3가지 방식 사용가능
  - 인라인 방식: 시작 tag 안에 style 속성 이용
  ```html
  <p style = "color:red"> hello </p>
  ```
  - internal 방식
  ```html
  <head>
    <style>
      CSS 설정
    </style>
  </head>
  ```

  - external 방식: 외부파일(CSS) 생성
  ```html
  <!-- external 방식 -->
  <link rel="stylesheet" type="text/css" href="css/mystyle.css">
  ```
