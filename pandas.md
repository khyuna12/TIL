## **pandas**

<br>
- 데이터 프레임

<br>

|컬럼|컬럼|컬럼|컬럼|
|--|--|--|--|
|10|.|.|.|
|20|.|.|.|
|30|.|.|.|

<br>

---

<br>

### 1. 데이터 프레임 생성 방법

   - **파일**에서 읽기 (많이 하는 방법)
```python
df = pd.read_csv('./data/file_name.csv')
```
   - **dict** 이용  
     - `df = pd.DataFrame(dict)`

```python
df = pd.DataFrame({"col1" : [4 ,5, 6],
                   "col2" : [7, 8, 9],
                   "col3" : [10, 11, 12]})

'''
   col1  col2  col3
0     4     7    10
1     5     8    11
2     6     9    12 
'''
```
   - **중첩 리스트**
     - `df = pd.DataFrame(중첩리스트, index=[], columns=[])`

```python
df = pd.DataFrame([[4, 7, 10],[5, 8, 11],[6, 9, 12]],
                  index=[1, 2, 3],
                  columns=['col1', 'col2', 'col3'])

'''
   col1  col2  col3
1     4     7    10
2     5     8    11
3     6     9    12
'''
```
   - **Series** 이용
```python
name =     pd.Series(["유관순","안중근"])
age =      pd.Series([18,31])
birthday = pd.Series(['1920/09/28','1910/03/26'])

hero = pd.DataFrame([name,age,birthday])
hero.columns =["hero1", "hero2"]
hero.index =["이름","나이","생일"]
print(hero)
'''
         hero1       hero2
이름         유관순         안중근
나이          18          31
생일  1920/09/28  1910/03/26
'''
```

<br>

+) 행,열 바꾸기
```python
print(hero.T) 
'''
        이름  나이          생일
hero1  유관순  18  1920/09/28
hero2  안중근  31  1910/03/26
'''
```

<br>

---

<br>
  
### 2. 인덱스 관리

- DataFrame 속성
   - 컬럼정보: `df.columns` 또는 `df.keys()`

   - 인덱스(라벨) 정보: `df.index`

   - 값 정보: `df.values` 또는 `df.to_numpy()`

<br>

0. 인덱스 변경
```python
df.index=[값, ...]
```
    
1. `df.set_index(기존컬럼, inplace=True|False)`
    
```python
df.reset_index(drop=False, inplace=True) # 기존 index를 컬럼으로 변경하고 새로운 index 생성
df.reset_index(drop=True, inplace=True) # 기존 index를 삭제하고 새로운 index 생성
```
           
2. `df.reindex(index=값)`  ==> 기존 index 재배치
    
3. `ignore_index = True`  ==> df와 df2 연결시 index도 연결이 되서 중복될 때 index는 빼고 연결하는 방법 (자동으로 index 생성됨)

<br>

---

<br>

### 3. 색인

<br>

**가. [ ]** : 인덱싱 연산자, 컬럼(들)을 선택하는 목적  
        예> `[컬럼]` ==> *Series* 반환 ( index와 값 으로 구성됨 )  
            `[[컬럼,컬럼]]` ==> *DataFrame* 반환
              
  - **단일컬럼 조회**
     - `df['컬럼명']`, Series로 반환  
     - `df.컬럼명`
        
  - **다중컬럼 조회**
     - `df[['컬럼명','컬럼명']]`, DataFrame 반환

**나. .loc** :  **label**만을 사용한다. ( 기본적으로 index의 label로 인식 )  
               label은 *single, list, slice* 형태 모두 가능하다.  
               행과 열을 동시에 조회할 수 있다.   
```python
df.loc[행,열]
```
               
**다.  .iloc** :   loc와 유사하지만 **정수위치값**만을 사용한다.  
                   행과 컬럼 모두 위치값 만 사용 가능하다.  
  - DataFrame 의 행(들) 조회 ==> SQL의  selection 기능

<br>

---

<br>

### 4. 컬럼 추가,삽입 및 삭제

<br>

- DataFrame에 **컬럼 추가**   
   ==> 기존 컬럼 값을 가지고 추가 정보를 얻을 떄

  - `df['컬럼명'] = 리스트`  
    `df['컬럼명'] = Series`
      
  - `new_df = df.assign(컬럼명=리스트)`
  - `new_df = df.assign(컬럼명=함수, 컬럼명=함수)`
  - `new_df = pd.concat([df,df2], axis=1)`

- DataFrame에 **컬럼 삽입**

  - `df.insert(idx, 컬럼명, 값 )`

<br>

- **컬럼 삭제**

   - 단일컬럼 삭제
      - `df.pop('컬럼명')`
      - `del df['컬럼명']`

    
  - 다중컬럼 삭제
     - `df.drop(columns=리스트)`
     - `df.drop(리스트, axis=1)`

<br>

### 5. 행 추가 및 삭제

<br>

- DataFrame **행(row) 추가**

  - 한번에 하나씩 추가   
    `new_df = df._append(df2, ignore_index=True)`     
    --> 버전업 1.3.0 이후에는 _append로 바뀜

  - 한번에 여러개 추가  
    `new_df = pd.concat([df,df2,..], axis=0 , ignore_index=True)`


- DataFrame **행 삭제**

  - `new_df = df.drop(index=[인덱스명, 인덱스명])`

  - `new_df = df.drop([인덱스명, 인덱스명], axis=0)`

<br>

---

<br>

## **null**

<br>

### 1. null값 **조회**

<br>

   -  Pandas 함수 이용
      - `bool = pd.isna(스칼라|Series|df)`
      - `bool = pd.isnull(스칼라|Series|df)`
      - `bool = pd.notnull(스칼라|Series|df)`

   -  DataFrame 함수 이용
      - `bool = df.isnull()`
      - `bool = df[컬럼명].isnull()`
      - `bool = df[[컬럼,컬럼2]].isnull()`

<br>

### 2. null값 **삭제**

<br>

   - 행 삭제
      - `new_df = df.dropna(axis=0|'index', inplace=False)`
      - `new_df = df.dropna(axis=0|'index', how="any|all", inplace=False)`


   - 열 삭제
      - `new_df = df.dropna(axis=1|'column', inplace=False)`
      - `new_df = df.dropna(axis=1|'column', how="any|all" , inplace=False)`
   
<br>

### 3. null값 **변경**

<br>

- `df.fillna(value, method='bfill|ffill|None', inplace=False, limit=n )`

<br>

---

<br>

### **DataFrame, Series 함수**

- **기술통계 함수**
   - 최대(소)값         ==>  `df.max(), df.min()`  
   - 누적최대(소)값,     ==>  `df.cummax(), df.cummin()` 
   - 최대(소)값label   ==>  `df.idxmax(), df.idxmin()`  
   - (누적)합계         ==>  `df.sum(), df.cumsum()`  
   - 평균              ==>  `df.mean()`  
   - 중앙값            ==>  `df.median()`  
   - (누적)곱          ==>  `df.prod(), df.cumprod()`  
   - 사분위             ==>  `df.quantile()`  
   - 분산               ==>  `df.var()`  
   - 표준편차           ==>  `df.std()`
   - count(갯수)         ==>  `df.count()`
   - 통합 통계           ==>  `df.describe()`

- **기본 함수**
   - 값 변경            ==>  `df.replace()`  
   - 컬럼명 및 인덱스명 변경 ==> `df.rename(columns|index)`
   - 모든(특정) 컬럼(행)값의 참/거짓 여부 ==>  `df.any() , df.all()`
   - 중복조회 및 제거   ==>  `df.duplicated()`,  `df.drop_duplicates()`

   - 임의의 함수 적용 ==> `df.apply(함수, axis=0|1)`
      임의의 함수를 한번에 DataFrame의 행과 열에 적용.

   - 값이 있으면 True, 아니면 False ==>`df.isin(집합형)`

   - unique한 값의 갯수 ==> `df.nunique(dropna=True)`
                              dropna=False 면 nan 포함해서 **개수**반환

   - `df['col1'].value_counts()` ==> 값의 빈도수 반환

   - `df['col1].unique` ==> 유니크 값 반환, **series만** 사용가능
    
   - `df['col1'].between(start, end)` ==> 범위에 있으면 True, 없으면 False, **series만** 사용가능

<br>

---

<br>


### **Series의 문자열 처리**
   
   - series.str.함수

```python
from pandas import Series
print(dir(Series.str))
'''
['capitalize', 'casefold', 'cat', 'center', 'contains', 'count', 
'decode', 'encode', 'endswith', 'extract', 'extractall', 
'find', 'findall', 'fullmatch', 'get', 'get_dummies', 
'index', 'isalnum', 'isalpha', 'isdecimal', 'isdigit', 'islower', 
'isnumeric', 'isspace', 'istitle', 'isupper', 'join', 'len', 'ljust', 'lower', 'lstrip', 
'match', 'normalize', 'pad', 'partition', 'removeprefix', 'removesuffix', 'repeat', 
'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 
'slice', 'slice_replace', 'split', 'startswith', 'strip', 'swapcase', 
'title', 'translate', 'upper', 'wrap', 'zfill']
'''
```

<br> 

   **<문자열 관련 함수>**
   - **python**
     - `문자열.함수`  
      예) "hello".upper()
   - **numpy**  
     - `arr = np.array(['aa', 'Bb', 'cc'])`  
    => `np.char.함수명`
   - **pandas**  
     - `series.str.함수`

