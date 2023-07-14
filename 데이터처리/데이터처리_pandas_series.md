ju## 데이터 다루기

1. 생성(데이터 타입)
    - Series(1차원)
    - DataFrame(2차원)

2. 필요한 데이터 찾아서 추출하기

3. 변경, 수정, 삭제

4. DF 연산, 병합

5. 함수 사용

<br>

---

<br>

## **pandas**

- **Series**, **DataFrame**등의 자료구조를 활용한 데이터 분석 기능을 제공해주는 라이브러리
```python
import pandas as pd
import numpy as np
```

<br>

### **Series**
- pandas 기본 객체 중 하나
- numpy의 `ndarray`를 기반으로 인덱싱을 기능을 추가하여 1차원 배열을 나타냄
- index를 지정하지 않을 시, 기본적으로 `ndarray`와 같이 0-based 인덱스 생성
- 같은 타입의 0개 이상의 데이터를 가질 수 있음

<br>

1. **자료구조: 시리즈**
- 데이터가 순차적으로 나열된 **1차원** 배열 형태
- 인덱스와 데이터 값이 일대일로 대응
- 딕셔너리와 비슷한 구조: `{key(index): value}`

<br>

2. **시리즈 생성**
- `Series()`
- **리스트**로 시리즈 만들기
```python
s = pd.Series([1,2,3])
```
- **딕셔너리**로 만들기
```python
scores={'홍길동':96, '이몽룡': 100, '성춘향':88}
s = pd.Series(scores)
```
- **튜플**로 만들기
```python
s = pd.Series((1.0,2.0,3.0))
```

<br>

3. **시리즈의 인덱스**
- 데이터 값의 위치를 나타내는 이름표 역할
- 문자열도 가능
```python
s = pd.Series([10,20,30], index=[1,2,3])
s = pd.Series([10,20,30], index=['홍길동','이몽룡','성춘향'])
```
```python
city = {'서울': 9631482, '부산':3393191, '인천':2632035, '대전':1490158}
s = pd.Series(city, index=city.keys())
```

- `시리즈.index`
```python
s = pd.Series([1,2,3]) # index 명시하지 않을시
s.index  # 범위 인덱스 생성
# RangeIndex(start=0, stop=3, step=1)
```
```python
s = pd.Series([99999, 88888, 77777, 66666], index=['서울', '부산', '인천', '대구'])
s.index  # Index(['서울', '부산', '인천', '대구'], dtype='object')
```

- `시리즈.index.name` 속성: 인덱스 이름 지정
```python
s.index.name = '광역시'
```
```python
s.index  # Index(['서울','부산','인천'], dytpe='object', name='광역시')
```

- `시리즈.values`: 시리즈의 값(numpy의 자료구조인 array 형태)
```python
s.values  # array([1,2,3], dtype=int64)
```

- `시리즈.name`
```python
s.name = '인구'
```

- **인덱싱**: 데이터에서 특정한 데이터 골라내는 것
    - 정수형 위치 인덱스
    - 인덱스 이름 또는 인덱스 라벨

```python
s['인천']  # 77777
```

```python
s[2]  # 77777
```

```python
s[0],s[3],s[1]  # (99999, 66666, 88888) tuple로 반환
s[[0, 3, 1]]  # 시리즈로 반환
s[1:3] # 시리즈 슬라이싱: 시리즈로 반환
```

- 정수형 인덱스를 명시 했을 경우
```python
s1 = pd.Series([100,200,300,400], index=[1,2,3,4])
# 슬라이싱은 0-base 슬라이싱
s1[2:4]  # index 3,4 시리즈로 반환
```
- 시리즈의 인덱스는 문자형으로 명시 권장

<br>

4. **시리즈 연산**

- **벡터화 연산**: 집합적 자료형 원소 각각을 독립적으로 계산(numpy 배열처럼)
```python
pd.Series([1,2,3]) + 4
```
```python
(s0>=7).sum() # True의 개수 총 합
(s0[s0>=7]).sum() # 조건의 결과가 True인 원소들의 합
```

- 인덱스가 같은 것끼리 연산
```python
num_s1 = pd.Series([1,2,3,4], index=['a','b','c','d'])
num_s2 = pd.Series([5,6,7,8], index=['b','c','d','a'])
num_s1 + num_s2
'''
a     9
b     7
c     9
d    11
dtype: int64
'''
```
```python
num_s3 = pd.Series([5,6,7,8], index=['e','b','f','g'])
num_s4 = pd.Series([1,2,3,4], index=['a','b','c','d'])
num_s3 - num_s4
'''
a    NaN
b    4.0
c    NaN
d    NaN
e    NaN
f    NaN
g    NaN
dtype: float64
'''
```
- `values` 속성 
```python
num_s3.values - num_s4.values
# array([4, 4, 4, 4], dtype=int64)
```

<br>

5. **딕셔너리와 시리즈**
- 시리즈는 라벨에 의해 인덱싱 가능
- 라벨을 key로 가지는 딕셔너리 형과 같음
- 딕셔너리에서 제공하는 대부분의 연산자 사용 가능(`in`연산자, `for`루프)
```python
'서울' in s  # True
```
```python
list(s.items())  # [('서울', 99999), ('부산', 88888), ('인천', 77777), ('대구', 66666)]
```
```python
for k, v in s.items():
    print('%s=%d' % (k,v))
'''
서울=99999
부산=88888
인천=77777
대구=66666
'''
```

- 딕셔너리로 시리즈 만들기
    - `Series({key:value, key:value, ...})`
    - index -> key
    - 값 -> value

```python
scores={'홍길동':96, '이몽룡': 100, '성춘향':88}
s = pd.Series(scores)
```

- 딕셔너리의 원소는 순서 없음, 딕셔너리로 생성된 시리즈도 마찬가지
```python
# 순서 보장하고 싶으면 인덱스를 리스트로 지정
city = {'서울': 9631482, '부산':3393191, '인천':2632035, '대전':1490158}
s = pd.Series(city, index=city.keys())
s = pd.Series(city, index=['부산', '인천', '서울', '대전'])
```

<br>

6. **시리즈 데이터의 갱신, 추가, 삭제**
- **인덱싱** 이용
```python
s['부산'] = 1630000
```
```python
del s['서울']
```

<br>

7. **Series 함수**
- `size`(속성): 개수
- `shape`(속성): 튜플 형태로 shape 반환
- `unique`: 유일한 값만 ndarray로 반환
- `count`: NaN을 제외한 개수 반환
- `mean`: NaN을 제외한 평균
- `value_counts`: NaN을 제외하고 각 값들의 빈도를 반환

```python
s1 = pd.Series([1,1,2,1,2,2,2,1,1,3,3,4,5,5,7,np.NaN])
```
```python
len(s1)  # 16
s1.size  # 16
s1.shape # (16,)
s1.unique()  # nan도 하나의 값으로 봄 array([ 1.,  2.,  3.,  4.,  5.,  7., nan])
s1.count()  # nan제외, 15
```
```python
a = np.array([2,2,2,2,np.NaN]) # array 타입
a.mean()  # nan
```
```python
b = pd.Series(a)
b.mean()  # 2.0
```