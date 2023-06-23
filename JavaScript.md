## JavaScript
> 웹 문서를 동적으로 바꾸거나 사용자가 입력한 폼 데이터의 유효성 검사기능을 포함하는 **동적**인 웹 어플리케이션 개발을 가능하게 해줌

<br>

### 1. ECMAScript6
  - 표준화된 스크립트 프로그래밍 언어
  - 비브라우저 실행 가능한 플랫폼(Node js)으로 자바스크립트 실행

<br>

### 2. 사용 방법
  - `head`, `body` 태그 안에 여러번 사용가능(`script` 태그 사용)
```html
<script>
  // 주석
  console.log("Javascript_body");  // f12 > console에 Javascript
</script>
```
  - 외부파일 접근
```html
<script src="external.js"></script>
```

<br>

### 3. **Data Type** - python과 비교 
  - python
    - 정수: `int`
    - 실수: `float`
    - 문자: `str`, `bytes`
    - 논리: `bool`(True, False)
    - null: `None`

  
  - **JS**
    - 정수&실수: `number`
    - 문자: `string`
    - 논리: `boolean`(true, false)
    - `null`
    - `undefined`
    - `NaN`(Not a Number)

  <br>

  - **참조형** 데이터 타입
    - (JSON) 배열객체: `[값, 값]`
    - JSON 객체: `{key: value}`
    - 함수(일급객체): `function(){}`
    - 클래스

<br>

### 4. 변수

  - python
    - 모든 변수는 참조변수
    - `변수명 = 값`: *변수명 선언*과 *변수에 값 저장(초기화)*을 한꺼번에
    - 변수 중복 가능

    <br>

  - **JS** 
    - *변수 선언*(영역 생성)
      - `var 변수명;`
      - `let 변수명;`
    ```js
    var n;
    console.log(n);  //undefined
    ```
    
    - *초기화*
        - `변수명=값`

    - 한꺼번에
    ```js
    // 기본형 데이터를 저장하는 변수(기본형 변수)
    var n = 3
    
    // 참조형 데이터를 저장하는 변수(참조형 변수)
    let x = [10, 20]
    ```
    
    - `let`
      - 변수 중복 선언이 불가능
      - ES6 버전 - 권장
      - 블럭 scope

    - `var`
      - 변수 중복 선언 가능
      - old 버전
      - 함수 scope: 함수 안에서 선언된 변수는 함수 안에서만 사용가능

<br>

+) python과 차이점 & 함수 scope, 블럭 scope 설명

  - python
    - 함수
    ```python
    def 함수명():
      들여쓰기
    ```

    - for, if문
    ```python
    for v in 집합형:
      들여쓰기

    if 조건문:
      들여쓰기
    ```

    <br>

  - **JS** 
    - 함수
    ```js
    function 함수명(){
      // 들여쓰기 대신 {}로 블럭
      var n = 10;
      let n2 = 20;
    } // var은 함수 scope이므로 {}밖에서 못 씀, let은 모든 블럭 밖에서 못 씀
    ```

    - for, if문
    ```js
    for(  ){
      var n = 10;
      let n2 = 20;
    } // var: 함수 블럭이 아니기 때문에 밖에서 사용 가능, let 사용 불가

    if(  ){
      var n = 10;
      let n2 = 20;
    } // var 사용 가능, let 사용 불가
    ```

<br>

### 5. 상수
  - 변수와 달리 값 변경 불가능

  ```js
  // 상수: 값 변경 불가
    const num = 10;
    // num = 20; console.log(num) 오류남
    console.log(num);  // 10
  ```

<br>

### 6. 연산자
> python과 다른 점 위주로

<br>

  - **연결 연산자** `+`
    - python에서는 문자열끼리만 가능
    - js는 문자열 + 비문자열|문자열
  ```js
  // 연산결과는 문자열
    let n = "hello" + "world";
    let n2 = "hello" + 10 + 20 + 30;
    let n3 = 10 + 20 + 30 + "hello";
    console.log(n)  // helloworld
    console.log(n2) // hello102030
    console.log(n3) // 60hello
  ```

<br>

  - **비교 연산자**
    - 자바스크립트에서 '같냐?'
	    - `==` (equal 연산자),  `!=` : 값만 비교
	    - `===` (identical 연산자),  `!==` :값과 타입까지 비교
  ```js
  console.log("equl: ", "10"==10); //true
  console.log("identical: ", "10"===10); // false
  ```

  <br>

  - **논리 연산자**
    - `&&` : and
      - 값1 `&&` 값2  
    ==> 값1이 true이면 값2 반환, false이면 값1 반환
    - `||` : or
      - 값1 `||` 값2  
    ==> 값1이 true이면 값1 반환, false이면 값2 반환
    - `!` : not

    - 다음의 5가지는 항상 논리값의 `false`로 처리한다.  
	    역으로 5가지가 아닌 것은 true로 처리한다.
	     - `0`
	     - `""`
	     - `null`
	     - `undefined`
	     - `NaN`
    
<br>

  - **증감 연산자**
    - 증가 연산자(1씩 증가): `n = n + 1` 과 동일
      - `++n`: 전치
      - `n++`: 후치

    - 감소 연산자(1씩 감소): `n = n - 1` 과 동일
      - `--n`: 전치
      - `n--`: 후치
    
    - *주의!* 다른 연산자와 같이 사용
      - `++n`: 먼저 증가 -> 변수 할당
      - `n++`: 먼저 변수 할당 -> 증가

    ```js
    var n = 10;
    var x = ++n;
    console.log(n, x);  // 11 11

    var n = 10;
    var x = n++;
    console.log(n, x);  // 11 10
    ```

<br>

  - **3항 연산자**
    - python: `변수 = 참 if 조건식 else 거짓`
    - **js**: `(조건식)? 참:거짓;`
      - 중첩 가능: `var x = (4>3)?(true)?100:200:"B";`

<br>

  - **spread 연산자**
    - 문법: `...배열|JSON`
    - 배열 복사
    ```js
    var n = [10,20,30];
    var n2 = [...n];
    ```

    - 특정 배열에 다른 배열 삽입
    ```js
    var x = [1,2,3];
    var n2 = [...n, ...x];  // 병합 효과
    console.log(n2);  // [10,20,30,1,2,3]
    ```

    - 기본에 특정값 추가
    ```js
    var x = [1,2,3];
    var n2 = [...x, 1000, 2000];
    console.log(n2);  // [1,2,3,1000,2000]
    ```

    - 문자열 펼치기
    ```js
    var n2 = [..."hello"]
    console.log(n2)  // ['h', 'e', 'l', 'l', 'o']
    ```

<br>

### 7.  조건문

  - **다중 if 문**
  ```js
  var n = prompt("정수: ")

    if(n>=90){
      console.log("A")
    } else if(n>=80){
      console.log("B")
    } else if(n>=70){
      console.log("C")
    }else {
      console.log("F")
    }
  ```

  - **switch 문**(다중 비교)
    - `break`는 옵션
  ```js
  switch(변수) {
    case 값1: 실행문; break;
    case 값2: 실행문; break;
    default: 실행문; break;
  }
  ```

<br>

### 8.  반복문

  - **while문**
    - 조건식이 false라면 문장이 한번도 실행되지 않음

  ```js
  시작값
  while(조건식){
    문장;
    증가/감소 연산자;
  }
  ```

  - **do while문**
    - 문장이 적어도 한번은 실행됨
  ```js
  시작값
  do{
    문장;
    증가/감소 연산자;
  } while(조건식);
  ```

- **for문**

  - python
```python
for 변수 in 집합형:
  문장
```

  - **JS**
    - 시작값, 조건식, 증감식이 있어야 함
    - 작동방식: 시작값 -> 조건식 -> 문장 -> 증감식 -> 조건식 (조건이 만족하지 않을 때까지 반복)
```js
for(시작값;조건식;증감식){
    문장
  }
```
  - while문과 달리 반복횟수 예측 쉽다 
  - 모든 제어문은 중첩 가능
```js
for(var n=1; n<=5; n++){  // 5번
    for (let m=0; m<2; m++){  // 2번
      console.log("A")  // 10번
    }
  }
```

- 반복문 빠져나오기
  - python
```python
# break
for 변수 in 집합형:
  문장
  if 조건식: break

# continue
for 변수 in 집합형:
  문장1
  문장2
  if 조건식: continue  # 조건식 맞으면 문장3 스킵됨
  문장3 
```

  - **JS**
    - python과 비슷
  ```js
  // break
  for(  ;  ;  ){
    문장
    if(조건식) break;
  }

  // continue
  for(  ;  ;  ){
    문장1;
    문장2;
    if(조건식) continue; // 조건식 맞으면 문장3 스킵됨
    문장3;
  }
  ```

<br>

### 9. 객체
> 첫글자 대문자, 사용하려면 생성 필수!

<br>

- **속성**: property(변수)
- **동작**: method(함수)

- **종류**
  - **시스템 정의 객체**(내장 객체, 빌트인 객체)
    - **Data** 관련 객체: *사용하려면 반드시 명시적으로 생성해야 함*
      - 수치 관련 객체: `Number`
      - 문자열 관련 객체: `String`
      - 날짜 관련 객체: `Date`
      - 논리 관련 객체: `Boolean`
      - 배열: `Array`
    
    - **브라우저** 관련 객체(BOM): *브라우저를 시작하면 자동 생성됨*
      - `Window`: 창, **전역 객체(최상위 객체)** 이기 때문에 `window.` 생략가능
        - 객체를 참조하는 변수: `window`(자동 생성됐기 때문에 정해져있음.)
        - Window 객체에 있는 함수/property: `alert()`, `prompt()`, `parseInt()`, `navigator`, `screen`, `location`, `history`, `document`
      - `Screen`: 화면의 크기(너비, 높이)
        - 객체 참조 변수: `screen`
      - `Navigator`: 브라우저 정보(크롬, 엣지, ...)
        - 객체 참조 변수: `navigator`
      - `History`: 뒤로가기, 앞으로 가기
        - 객체 참조 변수: `history`
      - `Location`: 브라우저의 url
        - 객체 참조 변수: `location`
        - `location.href`: JS로 링크 만들 수 있음(중요)

    - **문서(html)** 관련 객체(DOM): *브라우저에 html문서를 open할 때 tag에 해당되는 객체가 자동생성됨*
      - DOM 트리 이용해서 node 접근하고 값 변경/수정/삭제/추가
      - `Document`
        - property
        - method
          - id로 접근: `document.getElementById("id값")` -> 중첩된 태그가 있다면 같이 반환
          - CSS 선택자로 접근: `document.querySelector("선택자")`, `document.querySelectorAll("선택자")` -> 현재 태그부터 중첩된 태그, 값까지 반환  
          예: `document.querySelector(".클래스명")`, `document.querySelector("#id값")`
        - 반환 값이 객체라면 속성 사용 가능(태그의 속성도 가능)  
        예: `document.getElementById("x").innerText`, `document.querySelector(".y").innerHTML = "<h1>JS</h1>";`(값 변경)
      - *tag에서 필요한 값 얻기*
        - `.innerText`, `.innerHTML` (`div`는 `innerText` 안 됨)
        - 사용자 입력 form 태그: `.value`
        - 속성값 얻기 : `<tag property="property_value">` 일 때
        `.property`

  - **사용자 정의 객체**
    - JSON(JavaScript Object Notation): `{key : value}`(배열도 포함하지만 일반적으로 {key:value}를 뜻함)
    - 클래스

<br>

- 객체 **생성**

  ```js
  let str = new String("hello")  // python은 new 없었음
  let str = "hello"  // 일반적
  ```

- 객체의 **property와 method 확인**
  - w3schools.com 확인
  - `console.dir(str);`-> [prototype] 펼치기

- **propert** 사용
```js
console.log(str.length);  // 괄호 안씀
```

- **method** 사용
```js
console.log(str.charAt(0));  // 0번째에 있는 문자 반환
```

<br>

> 배열 객체 & for문

- python
```python
for 변수 in [1,2,3]:
  문장

# 위치
for idx, value in enumerate([1,2,3]):
  문장
```

- **JS**
```js
// 일반 for문 이용
for(var i=0; i < arr2.length; i++){
  console.log(arr2[i]);
} // 10 20 30 

// for~of문(변수에 배열의 값 저장)
for(let x of arr2){
  console.log(x);
} // 10 20 30

// for~in문(변수에 배열의 index 저장)
for(let x in arr2){
  console.log(x);
} // 0 1 2
```

<br>

### 10. 함수

  - 함수 표현식(이름 없는 함수)
    - python에선 `lambda`
```js
var 변수 = function ([변수, ...]){
  문장;
  [return 값];
}
```

  - 함수 선언식(이름 있는 함수)
    - 매개변수랑 인수(호출 시 넣는 값) 개수 달라도 됨
```js
function 함수명([변수, ...]){
  문장;
  [return 값];
}
```

  - **가변인자**
```js
var fun2 = function(...n){  // rest 파라미터, 가변인자
  console.log(n);
}

// 호출
fun2(10);        // [10]
fun2(1,2,3);     // [1, 2, 3]
fun2(1,2,3,5,7); // [1, 2, 3, 5, 7]
```

- default 파라미터 & 가변인자

```js
function fun3(n=1,n2=2, ...n3){
  console.log(n, n2, n3)
}

fun3(10);        // 10 2 []
fun3(1,2,3);     // 1 2 [3]
fun3(1,2,3,5,7); // 1 2 [3, 5, 7]
```

- **arrow 함수**
```js
// JavaScript
var x = (n, n2) => n + n2;
```

```python
# python
x = lambda n,n2: n+n2
```

<br>

### 11. 이벤트(event)
  - 특별한 사건
  - **이벤트 발생 주체**
    - 사용자
      - 마우스 - 버튼 클릭/더블클릭/드래그/마우스 오버/마우스 아웃
      - 키보드 - 입력
    - 시스템
      - 웹브라우저가 html 문서를 보고 모든 DOM tree를 만들었을 때

  - **이벤트 소스**
    - 이벤트가 발생한 곳(태그)  
    예: `<button>ok</button>`

  - **이벤트 타입**
    - 클릭: click 이벤트 타입

  - **이벤트 핸들러**
    - 발생된 이벤트 타입과 실제 처리하는 함수를 연결하는 역할
    - `on이벤트타입 = 함수`: **이벤트 소스**에 설정
      - `onclick`
      - `onmouseover`
      - `onmouseout`
      - `onkeyup`
      - 이벤트 발생 주체가 시스템==> `onload`: body에 주로 씀
```html
<button onclick="fun()">OK</button>
<select name="cars" onchange="fun()">         <!-- 선택지 바꿀때마다 -->
    <option value="">선택하시오</option>
    <option value="volvo">볼보</option>
    <option value="saab">사브</option>
    <option value="audi">아우디</option>
</select>
<input type="text" name="username" onkeyup="fun()" onmouseover="fun()" onmouseout="fun()">
<!--onkeyup: 누르고 떼면-->
```

- **이벤트 객체**
  - 이벤트 발생 시 자동 생성
  - `event.preventDefault()`: (중요) 무조건 동작되는 기능(submit, a href) 방지
  - `event.stopPropagation()`: 태그 중첩되어 있을 때 이벤트 전파 방지

```js
function fun2(){
      event.preventDefault();
}
```
```html
<form action="target.html" onsubmit="fun2()">
	이름 <input type="text" name="username"><br>
	나이 <input type="text" name="age">
	<input type="submit" value="전송">
</form> 
```
-> 전송 버튼 눌러도 안 넘어감

<br>

### 12. template literal

- 문자열 작성 방법
  - ""
  - ''
  - ``(back-tick)

- 쌍따옴표와 홑따옴표
  - 문자열이 라인 넘어갈 때마다 `\` 필요, 모양 유지 안 됨
  - 따라서 문자열 안에 html 쓰면 가독성 안 좋음
  - 문자열 중간에 변수 삽입할 때 `+` 써야 함

- ``(back-tick)
  - enter 사용가능
  - 모양 유지 가능
  - `${변수명}` 으로 변수 삽입 가능

<br>

### 13. Ajax(Asynchronous Javascript And Xml)

- **비동기(<=> 동기)** 자바스크립트와 **데이터(Xml, *JSON*)**
- **동기** 방식(현재 사용중인 방식)
  - 순서대로 동작하는 방식
  - 브라우저가 서버에 파일을 요청하면 서버는 브라우저가 요청한 파일 찾고 html로 돌려줌
  - 요청 -> search -> 응답(**전체html**)
  - **장단점**
    - 전체화면 리로딩, 성능 떨어짐
    - 작업 순서 보장(결제할 때는 좋음)

- **비동기** 방식(Ajax)
  - 브라우저가 서버에 파일을 요청하고 서버는 search, 브라우저는 안 기다리고 제 할 일 하는 도중에 서버 응답(html이 아니라 바뀔 **Data**만)
  - **장단점**
    - 화면 일부분만 리로딩,  성능 좋음
    - 순서 보장 안됨, 작업 순서가 중요한 작업은 동기 방식으로 진행해야 함
  - `XMLHttpRequest` 객체 이용
    - property
    - method

  - **실습**
    - [참고 사이트](https://reqres.in/)
    - `https://reqres.in/`에 request 붙여넣기해서 data 얻기

  ```js
  var httpRequest;  // 함수 밖에서도 써야 함
  function req(){
    // 1. 객체 생성
    httpRequest = new XMLHttpRequest();
    console.dir(httpRequest);

    // 2. 응답시 처리할 수 있는 콜백함수 호출하는 이벤트 핸들러 등록
    httpRequest.onreadystatechange = responseFun;  // 괄호 X

    // 3. url 정보 및 추가 정보 설정
    httpRequest.open("get", "https://reqres.in/api/users/2");  // get방식으로 url 요청하겠다

    // 4. 요청
    httpRequest.send(null);  // get 방식인 경우는 null 지정
    }
  ```

  ```js
  // 응답하는 함수
  function responseFun(){
    // 성공인 경우에만 처리
    if(httpRequest.status == 200 && httpRequest.readyState == 4){
      var data = httpRequest.responseText;
      console.log(data, typeof data);

      var jsonData = JSON.parse(data);
      console.log(jsonData, typeof jsonData);

      var id = jsonData.data.id;
      var email = jsonData.data.email;
      var first_name = jsonData.data.first_name;
      var last_name = jsonData.data.last_name;
      var avatar = jsonData.data.avatar;
      console.log(id, email, first_name, last_name, avatar);

      var table = `<table>
                    <tr>
                      <th>id</th>
                      <th>email</th>
                      <th>first_name</th>
                      <th>last_name</th>
                      <th>avatar</th>
                    </tr> 
                    <tr>
                      <td>${id}</td>
                      <td>${email}</td>
                      <td>${first_name}</td>
                      <td>${last_name}</td>
                      <td><img src="${avatar}" width="100" height="100"></td>
                    </tr>
                  </table>`;
      document.querySelector("#result").innerHTML = table;
    }
  }
  ```

  <br>

### 14. 객체분해할당

- 객체(배열 JSON)를 분해해서 변수로 할당

- **배열**
```js
let[a,b,c] = [10,20,30]

var[a,b,c] = [10,20];  // c는 undefined
```

- **json**
```js
var {a,b} = {a:100, b:200};
```