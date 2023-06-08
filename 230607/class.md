## class 변수와 메서드

```python
class 클래스명:

	변수 = 값  # 클래스 변수
    
    def __init__(self, n):
    	self.name = n   # 인스턴스 변수, 객체 생성시 생성(매번), 변수명. 접근
        
    def methond(Self): # 인스턴스 메서드(regular method), 변수명. 접근
    	pass
        
    @classmethod
    def method(cls):  # 클래스 메서드
    	pass
```

---

1. class 변수
  - 단 한번만 생성
  - 클래스명. 접근



2. class 메서드
  - 목적: 객체 생성 없이 사용하기 위해서
  - 클래스명. 접근

---

### 예

```python
class Person:

    address = "서울"  # 클래스 변수

    def __init__(self, n, a):
        # 인스턴스 변수
        self.username = n
        self.age = a

    def info(self):  # 인스턴스 메서드
        return self.username, self.age, Person.address

    # 클래스 메서드
    @classmethod
    def get_address(cls):
        return Person.address

Person.address = "제주"  # 한번에 모든 address 변경이 된다
p = Person("홍길동", 20)
p2 = Person("이순신", 40)

print("p1:", p.info(), Person.get_address())  # p1: ('홍길동', 20, '제주') 제주
print("p2:", p2.info(), Person.get_address())  # p2: ('이순신', 40, '제주') 제주
```
