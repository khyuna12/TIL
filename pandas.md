## pandas

<br>
- 데이터 프레임

|컬럼|컬럼|컬럼|컬럼|
|--|--|--|--|
|10|.|.|.|
|20|.|.|.|
|30|.|.|.|

<br>

1. 데이터 프레임 생성 방법
   - 파일에서 읽기 (많이 하는 방법)
   - dict 이용  
     - df = pd.DataFrame(dict)
   - 중첩 리스트
     - df = pd.DataFrame(중첩리스트, index=[], columns=[])
   - Series 이용
2. 색인
   - loc[ ]
   - iloc[ ]