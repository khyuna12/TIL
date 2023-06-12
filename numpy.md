## Numpy
23.06.09
<br>

1. 다차원 배열 관리

2. 1차원 [ ], 벡터  
   2차원 [[ ]], 행렬  
   3차원이상 [[[ ]]], 텐서(tensor)

3. 관련 함수
   - `np.array(list)`
   - 랜덤함수
     - `np.random.seed()`
     - `np.random.random([n])`
     - `np.random.rand([n])`
     - `np.random.randn([n])`
     - `np.random.randint(low, high, n)`
     - `np.random.choice(list)`
     - `np.random.shuffle(list)`
   - 특정한 값으로 채우기
     - `np.zeros(shape)`  
     - `np.ones(shape)`  
     - `np.empty(shape)`  
     - `np.full(shape, 값)`
   - 범위: `np.arange([start], stop, [step])`
   - 동일한 간격: `np.linspace(start, stop, [num = 값, endpoint = True])`
   - 삭제 
     - `np.delete(arr, idx|fancy|slice, axis)`
     - `np.where(arr == 값)`
   - 삽입, 추가
     - `np.append(arr, values, axis=None)`
     - `np.insert(arr, idx|fancy|slice, value, axis)`

<br>

---

<br>
23.06.12
<br>

### **얕은 복사(주소값 복사)** vs **깊은 복사(실제값 복사)**

<br>

  1. **기본 python**

      - **얕은 복사**
      ```
      x = [1,2,3]  
      x2 = x 
      ```
      - x2에서 값 변경하면 x도 변경됨
            
      - python의 **깊은복사** 3가지 방법
      ```
      x3 = `x[:]`
      x3 = `x.copy()`
      x3 = `list(x)`
      ```
<br>

  2. **numpy**
      - `[:]`   
      슬라이싱 처리는 얕은 복사로 처리함  
      그런데 주소값은 다르다.   
      뷰 형태로 연결되어 있음.  
      따라서 값을 변경하면 원본값도 변경됨
             
      - numpy의 깊은복사 방법  
         - `np.copy(값)` 또는 `값.copy()`

<br>



<br>

## 다차원 **열병합**

<br>

  - 수평축을 기준으로 열 병합  

  - **튜플 형태로 들어간다는 거 주의**

  
   `np.hstack((arr, arr2))` ==> 수평(horizontal)방향으로 병합
   `np.concatenate((arr,arr2), axis=1 )` ==> axis=1인 컬럼방향으로 병합
   `np.column_stack((arr, arr2))` ==> 컬럼(column)방향으로 병합
  
<br>
    
## 다차원 **행병합**

<br>

   - 수직축을 기준으로 행 병합

   `np.vstack((arr, arr2))` ==> 수직(vertical)방향으로 병합  
   `np.concatenate((arr,arr2), axis=0 )` ==> axis=0인 행방향으로 병합  
   `np.row_stack((arr, arr2))` ==> 행(row)방향으로 병합

<br>



<br>

## 차원변경

<br>

**1. 차원증가** ( 1차원 --> 2차원)  
    **예>** [1 2 3] (3,) ==>[[1 2 3]] (1,3)

  - `arr1D.reshape((행,열))`
  - `np.expand_dims(arr1D, axis=0)`
  - `arr1D[np.newaxis, ...]`, `arr1D[np.newaxis, :]`

<br>

**2. 차원 감소** ( n차원 --> n-1차원)  
    **예>** [[1 2 3]] (1,3) => [1 2 3] (3,) 
  ```
  arr1D = np.squeeze(arr2D, axix=0)
  ```