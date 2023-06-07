## 예외  

- 프로그램 실행 중에 발생하는 문제  
<br></br>

## 예외처리

- 예외 발생 시 비정상 종료되는 코드를 정상 종료되게 하는 것

- 예외 클래스가 제공됨

```python
try:
  문장
  문장
except 예외클래스명 as 별칭:
  문장  # 예외 발생 시 처리
```

<br></br>

---

<br></br>

**예:** 예외 발생 사례
```python
print("1")
print("2")

n = 0
result = 10 / n  #여기서 멈춤
print("결과값:", result)

print("3")
print("end. 정상종료")
```

**결과:**  
ZeroDivisionError: division by zero  
1  
2  

<br></br>

**예외처리하기**

```python
print("1")
print("2")

try:
    n = 0
    result = 10 / n  #여기서 멈춤
    print("결과값:", result)
except ZeroDivisionError as e:  # 다른 예외클래스는 오류남. 단, 부모클래스는 가능(다형성)
    print("0으로 나눠 예외발생")

print("3")
print("end. 정상종료")
```

**결과:**  
1  
2  
0으로 나눠 예외발생  
3  
end. 정상종료

<br></br>

---

<br></br>

## 예외클래스
- Object
  - BaseException
    - Exception(예외의 최상위 클래스)
      - ArithmeticError
        - ZeroDivisionError
      - TypeError
      - ValueError
      - ...

**다형성을 이용해서 모든 예외를 Exception으로 사용할 수는 있으나 권장 안함.**

<br></br>

---

<br></br>

참고: 

[예외처리 참고링크](https://docs.python.org/3/tutorial/errors.html)