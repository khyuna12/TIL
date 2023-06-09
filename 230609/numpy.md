## Numpy

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