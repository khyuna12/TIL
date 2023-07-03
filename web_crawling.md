# Web crawling(웹 크롤링)과 scraping(스크레이핑)

> 크롤러: 자동으로 웹 페이지에 있는 정보를 수집하는 프로그램  
> 크롤링: 크롤러로 정보를 수집하는 것
>
> 스크레이핑: 수집한 정보를 분석해서 필요한 정보를 추출하는 것

<br>

## **크롤러의 처리 과정**

1. **수집**(request, response)
  - 데이터 요청
    - `webbrowser`
      - `webbrowser.open()`
    - `urllib`
      - `urlopen()`
      - `urlretrieve(파일 url, 다운받을 경로)`: 파일 저장된 경로와 header 반환
2. **파싱**
  - 텍스트 데이터 -> 구조화 데이터
  - HTML 구조화
  - `BeautifulSoup`
3. **추출**(scraping)
  - 구조화 데이터 추출
  - `find('태그', '속성')`, `find_all()`, `findAll()`
  - `select()`, `select_one()`: list로 반환
  - `get_text()`
  - `text`
  - `string`
4. **가공**
  - 가능한 데이터로 가공
5. **저장**
  - 데이터베이스에 저장
  - SQL로 검색 가능
6. **출력**
  - 시각화
  - 엑셀 

<br>

---

<br>

### **<웹 브라우저 실행>**
- 기본 웹브라우저 자동 실행, 해당 url 주소로 접속
```python
import webbrowser
webbrowser.open("www.url.com")
```
```python
True  
```

<br>

### **<웹 페이지 추출>**

- 표준 라이브러리 `urilib.request` 모듈 사용
- `urilib.request`의 `urlopen()`함수 이용
```python
from urllib.request import urlopen

 f = urlopen('http://url.co.kr')  # HTTPResponse 자료형의 객체 반환
```
```python
 type(f)
 f.read()  # read 메서드: HTTP 응답 본문(bytes 자료형) 추출
 f.status  # 상태 코드 추출
 f.getheader('Content-Type')  # HTTP 헤더의 값 추출
 ```

<br>

### **<웹 페이지에서 데이터 추출>**

- **웹 페이지의 HTML 소스 갖고 오기**
```python
import requests

r = requests.get("https://www.google.co.kr")  # <Response [200]>
r.text[0:100]  # 일부분 출력

```

<br>

#### **BeautifulSoup** 라이브러리
- HTML 소스 **파싱**
- 태그나 속성을 통해 원하는 데이터 추출

```python
from bs4 import BeautifulSoup

html = requests.get("https://www.google.co.kr").text

soup = BeautifulSoup(html, 'lxml')
print(soup.prettify())  # 파싱 결과 더 보기 편하게
```

- `find('태그',['속성'])`: 태그까지 같이 반환
- `find_all('태그',['속성'])`
- `get_text()`: 리스트에 적용 불가

```python
site_names = soup.find_all('a')
for site_name in site_names:
  print(site_name.get_text())
```

```python
# find 없이 태그 찾기(태그까지 같이 반환)
soup.title
soup.body
soup.body.h1
```

- 속성으로 찾기
```python
soup2 = BeautifulSoup(html2, "lxml")

book_titles = soup2.find_all('p', {"id":"book_title"})
authors = soup2.find_all('p', {"id":"author"})

for book_title, author in zip(book_titles, authors):
    print(book_title.get_text()+"/"+author.get_text())
```

- `select()`: `find()`와 달리 *리스트*로 반환
```python
soup2.select('body h1')
# [<h1>책 정보</h1>]
soup2.select('p#book_title' )
```
```python
soup3.select('a#naver')[0].get_text()  # select는 리스트로 반환되니까
# '네이버'
```
<br>

#### **이미지** 내려 받기
- `os.makedirs(folder)`: 이미지 파일을 내 컴퓨터로 내려받을 폴더 생성
- `os.path.exists(folder)`: 폴더 존재여부
```python
folder = "C:/Myexam/download"

if not os.path.exists(folder):
    os.makedirs(folder)
```

- `os.path.join(folder, file)`: 생성된 폴더와 추출한 이미지 파일명을 합치기
- `os.path.join(path1[, path2[, ...]])`
- `requests.get(url).iter_content(chunk_size)`: 전체 이미지를 chunk_size만큼 나눠서 내려받음
```python
imageFile = open(image_path, 'wb')
chunk_size = 1000000
for chunk in html_image.iter_content(chunk_size):
    imageFile.write(chunk)
imageFile.close()
```
- `os.listdir(folder)`: 지정된 폴더의 파일 목록 보여줌

- 이미지 내려받는 함수
```python
import requests
from bs4 import BeautifulSoup
import os

# URL에서 이미지 주소 추출
def get_image_url(url):
    html_image_url = requests.get(url).text
    soup_image_url = BeautifulSoup(html_image_url, "lxml")
    image_elements = soup_image_url.select('img')
    if(image_elements != None):
        image_urls = []
        for image_element in image_elements:
            image_urls.append(image_element.get("src"))
        return image_urls
    else:
        return None

# 폴더를 지정해 이미지 주소에서 이미지 내려받기
def download_image(img_folder, img_url):
    if(img_url != None):
        html_image = requests.get(img_url)
        # os.path.basename(URL)는 웹사이트나 폴더가 포함된 파일명에서 파일명만 분리
        imageFile = open(os.path.join(img_folder, os.path.basename(img_url)), 'wb')
        
        chunk_size = 1000000
        for chunk in html_image.iter_content(chunk_size):
            imageFile.write(chunk)
            imageFile.close()
        print("이미지 파일명: {0}. 내려받기 완료!".format(os.path.basename(img_url)))
    else:
        print("내려받을 이미지가 없습니다.")

# 웹 사이트의 주소 지정
reshot_url = 'https://www.reshot.com/search/animal'

figure_folder = "C:/Myexam/download" # 이미지를 내려받을 폴더 지정

reshot_image_urls = get_image_url(reshot_url) # 이미지 파일의 주소 가져오기

num_of_download_image = 7 # 내려받을 이미지 개수 지정
# num_of_download_image = len(reshot_image_url)

for k in range(num_of_download_image):
    download_image(figure_folder, reshot_image_urls[k])
print("========================")
print("선택한 모든 이미지 내려받기 완료!")
```

<br>

#### **XML 스크레이핑**
  - 블로그 또는 뉴스 웹사이트 등의 웹사이트는 변경 정보 등을 RSS라는 이름의 XML 형식으로 제공
  - html보다 간단히 파싱
  - 내부에 피드를 나타내는 channel 요소가 있음

<br>

#### **정규표현식**으로 스크레이핑
  - 표준 라이브러리의 re 모듈
```python
import re
from html import unescape
```

<br>

### **<데이터 저장하기>**
- csv 형식으로 저장
- JSON 형식으로 저장
- 데이터베이스에 저장

<br>

### **Selenium**
- 웹 자동화
- Chromedriver

- 필요한 라이브러리
```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service as ChromeService
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.by import By
```

- 브라우저 열기
```python
driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()))
```

- 웹 드라이버 객체 만들기 및 페이지 이동
```python
driver.get("https://www.naver.com/")  # 위에서 뜬 창 닫으면 안됨
```

- 브라우저 사이즈: `driver.set_window_size(1024, 768)`
- 브라우저의 스크롤 위치: `driver.execute_script("window.scrollTo(200,300);")`(자바스크립트)
- alert 다루기
  - 생성: `driver.execute_script("alert('내용');")`
  - 확인 버튼 누르기: `alert.accept()`
  - 체크:
  ```python
  try:
    alert = driver.switch_to.alert
    print(alert.text)
  except:
    print('alert 없음')
  ```

- 텍스트 데이터 가져오기
  - `find_element(By.CSS_SELECTOR, "classname")`
  - `find_elements(By.CSS_SELECTOR, "classname")`

<br>

---

<br>

### 웹 사이트에 접근시 / 수집한 데이터 다룰 때 주의 사항

- 웹 사이트 이용 규약 확인
- robots.txt와 robots 메타 태그의 접근 제한 사항 준수
- 상대 서버에 부하가 가지 않을 정도의 속도로 접근
- rel="nofollow"가 설정돼 있으면 접근 X
- 저작권 준수
- 수집한 데이터 기반 검색 서비스는 문제가 없을 때만 제공

<br>



