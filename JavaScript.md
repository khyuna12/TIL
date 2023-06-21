## JavaScript
> 웹 문서를 동적으로 바꾸거나 사용자가 입력한 폼 데이터의 유효성 검사기능을 포함하는 **동적**인 웹 어플리케이션 개발을 가능하게 해줌

<br>

### 1. ECMAScript6

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
  - while문과 달리 반복횟수 예측 가능
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

