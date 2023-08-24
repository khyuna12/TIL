## 웹 프로그래밍

### MVC(Model View Controller) 패턴(일반)

- 웹 서버를 만들 때 더 편하기 만들기 위한 것
- Model: DB
- View: HTML(데이터)
- Controller: function(데이터 처리)
- 한 요소가 다른 요소들에 영향을 주지 않도록 설계하는 방식

### MVT(Model View Template) 패턴(장고)

- **장고**: Model View Controller 기반으로 한 프레임워크
- **Model**: DB(사용될 데이터에 대한 정의를 담고 있는 장고의 **클래스**)
- **View**: function
- **Template**: 데이터를 가지고 있는 HTML로 구성(유저들한테 보여지는 UI)
- 패턴
  - 클라이언트로부터 요청받으면 URL분석(URL.conf)
  - URL 분석결과를 통해 해당 URL에 대한 처리를 담당할 view 결정
  - view는 자신의 로직을 실행하면서 model을 통해 처리하고 결과 반환
  - view는 로직 처리가 끝나면 Template을 사용하여 클라이언트에 전송할 HTML 생성
  - view는 최종 결과로 HTML파일을 클라이언트에 보냄

<br>

### **MVT 코딩 순서**

1. 프로젝트 뼈대 만들기
  - 프로젝트와 앱에 필요한 디렉토리와 파일 생성
  - `django-admin startproject mysite`: mysite라는 프로젝트 생성
  - `python manage.py startapp polls`: polls라는 앱 생성
  - `notepad settings.py`: 설정 파일 확인 및 수정
  - `python manage.py migrate`: 데이터베이스에 기본 테이블 생성
  - `python manage.py runserver`: 현재까지 작업 개발용 웹 서버로 확인

2. model 코딩
  - `models.py`
  - `admin.py`

3. URLconf 코딩하기
  - `urls.py`(project와 app의 파일 둘 다)

4. Template 코딩하기
  - `template/ * .html`  
    예)
    - `index.html`: 최근에 실시하고 있는 질문의 리스트
    - `detail.html`: 하나의 질문에 투표할 수 있도록 답변 항목 폼으로 보여줌
    - `results.html`: 질문에 따른 투표 결과

5. View 코딩
  - `views.py`