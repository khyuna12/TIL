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

- **DOM(Document Object Model)**
  - html문서에 있는 tag에 해당되는 객체를 생성하고 tree로 만드는 구조
  - node
    - element node
    - attribute node
    - text node

<br>

- **Query String**
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
<br>

- **경로 지정**(중요)
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
- html에서 **3가지 방식** 사용가능
  - **인라인** 방식: 시작 tag 안에 style 속성 이용
  ```html
  <p style = "color:red"> hello </p>
  ```
  - **internal** 방식
  ```html
  <head>
    <style>
      CSS 설정
    </style>
  </head>
  ```

  - **external** 방식: 외부파일(CSS) 생성
  ```html
  <!-- external 방식 -->
  <link rel="stylesheet" type="text/css" href="css/mystyle.css">
  ```

<br>

- **selector**
  - all: `*{}`
  - tag: `tag_name{}`
  - id: `#id_name{}`
  - class: `.class_name{}`
  - 자손 선택자: `parent child{}`
  - 자식 선택자: `parent > child{}`
  - 형제 선택자(하나만): `sibling + sibling{}`
  - 형제 선택자(모두): `sibling ~ sibling{}`
  - 속성 선택자: 
    - `[id]{}`
    - `a[id]{}`
    - `[id="one"]{}`
    - `a[href^='https']{}`: 특정문구로 시작
    - `a[href$='net']{}`
    - `div[class*='man']{}`: 특정문구 포함
  - pseudo
    - `a:link {}`: unvisited link
    - `a:visited {}`: visited link
    - `a:hover {}`: mouse over link
    - `a:active {}`: selected link
    - `p:first-child {}`: p 태그의 부모기준으로 첫 번째 p태그 반환
    - `p:last-child {}`: p 태그의 부모기준으로 마지막 p태그 반환
    - `p:only-child{}`: 유일한 자식으로 된 모든 p태그 선택
    - `p:nth-child(n){}` : n번째 자식으로 된 모든 p태그 선택
    - `tr:nth-child(even)`, `tr:nth-child(odd)`
    - `p:not(p:nth-child(n)){}`: n번째 자식이 아닌 모든 p태그 선택
    - `input:disabled{}`: 선택, 값 입력 불가
    - `input:enabled{}`
    - `input:checked{}`
    - `p:empty{}`

- **size**
  - `1em`: 현재 요소의 상대적 크기, 현재는 1em = 16px
  - `1rem`: root 요소의 상대적 크기, 현재는 1rem = 16px

- **display**
  - `display:none;`: 보이지도 않고 영역 유지도 안됨
  - `display: inline;`: inline이라 width, height 적용 불가
  - `display: inline-block;`: inline이지만 width, height 적용 가능

- **visibility**
  - `visibility: hidden;`: 보이지는 않지만 영역 유지
  - `visibility: collapse;`: 보이지도 않고 영역 유지도 안됨

- **opacity**
  - `opacity:0.2;`: 투명도. 0으로 갈수록 투명해짐

- **box model**
  - `width`: content의 너비
  - `height`: content의 높이
  - `border`: box 테두리(content 테두리 아님)
  - `padding`: 테두리 안쪽 여백
  - `margin`: 테두리 바깥쪽 여백
  - `box-sizintg: border-box;`: width와 height로 설정된 값에 padding,border,margin값이 포함(기본은 `content-box`)

- **background**
  - `background-image:url('images/001.png');`
  - `background-repeat: no-repeat;`
  - `background-attachment: fixed;`: scroll(스크롤해서 내려가면 안보임),fixed(scroll해도 이미지 보임)
  - `background-position: center;`
  - `background-color: powderblue;`
  - `background-size: cover;`: cover(이미지를 늘리거나 가장자리 중 하나를 약간 잘라야 하는 경우에도 전체 컨테이너를 덮도록 배경 이미지의 크기를 조정), contain(이미지가 완전히 보이도록 배경 이미지의 크기를 조정)

- **font**
  - `font: font-style font-weight font-size font-family`
  - 예: `font: italic bold 50px  Arial, Georgia, Times, "Times New Roman", serif;`

- **text**
  - `text-align: right;`: justify는 양쪽 정렬
  - `text-decoration: underline`: line-through는 취소선
  - `text-transform: uppercase;`: capitalizes는 앞글자만 대문자
  - `text-indent: 10px;`: 첫 줄 들여쓰기
  - `line-height: 5;`: 줄 간격
  - `letter-spacing: 3px;`
  - `word-spacing: 10px;`

- **position** + top, bottom, left, right
  - `static`: 기본, normal position, top, bottom, left, right 적용 불가
  - `relative`: normal position 기준
  - `absolute`: 부모 tag 기준
    - 부모요소에 height 속성을 설정한다
    - 부모요소에 relative position을 설정한다.(부모 요소가 없거나 부모요소에 position 설정값(static제외)을 설정하지 않으면
body 요소를 기준으로 설정된다. 따라서 scroll하면 움직이게 된다.)
    - 자식요소에 absolute position을 설정한다
  - `fixed`: 브라우저 화면(viewport) 기준

- **z-index**
  - `z-index: -1;`: 요소의 stack 순서를 변경할 수 있음. 큰 값을 입력할 수록 위로 올라옴.

- **float**
  - `float:left;`
  - `clear:both;`: 맨밑으로 내려감, float에 독립적

- **flex**
  - Flexbox 모듈을 적용하기 위해서는 기본적으로 부모/자식 관계를 설정해야함
  - 부모는 Flex Container 이고 그 안에 있는 모든 것이 자식인 Flex Item

  <br>

  - container
    - `display:flex;`
    - `flex-direction: column;`: row-reverse, column-reverse도 가능
    - `flex-wrap: wrap;`: no-wrap(브라우저 크기를 줄이면 플렉스 항목들의 크기가 자동으로 축소됨), wrap ( wrap-reverse) 으로 지정하면 Container의 여러 줄에 걸쳐서 보여진다.
    - `flex-flow: row wrap;`: flex-direction 속성과 flex-wrap 속성을 모두 설정하기 위한 단축표현 방법
    - `justify-content: space-around;`: 주 축에 대하여 정렬을 설정(flex-start, flex-end, space-evenly), row가 기본
    - `align-items: stretch;`: 교차 축에 대하여 정렬 설정(기본이 stretch)
    - `align-content: stretch;`
  - item
    - `order: 3`: 기본값은 0
    - `flex-basis: auto;`: 자신의 content 너비값으로 설정 (기본)/ width 값이 있으면 width값으로 설정, width, basis 둘다 값 있으면 basis
    - `flex-grow: 1;`: 기본값은 0 으로 나머지 Flex Item에 비해서 얼마나 더 커질지 지정
    - `flex-shrink: 1;`: flex-grow 속성과는 반대, 0으로 지정하면 축소 안됨
    - `flex: 0 0 200px;`: flex-grow, flex-shrink, flex-basis
    - `align-self: center;`: 독립적으로 적용

<br>

- **Media Query**
```css
@media  screen and (max-width: 600px) { /* 최대 600px 이 되면 lightblue로 변경해라 */
  body {
    background-color: lightblue;
  }
}
```