## 웹 프로그래밍

### **MVC(Model View Controller) 패턴(일반)**

- 웹 서버를 만들 때 더 편하기 만들기 위한 것
- Model: DB
- View: HTML(데이터)
- Controller: function(데이터 처리)
- 한 요소가 다른 요소들에 영향을 주지 않도록 설계하는 방식

<br>

---

<br>

## Django 웹 프레임워크

- Model View Controller 기반으로 한 프레임워크
  - view를 template, controller를 view라고 함
- 객체 관계 매핑(ORM, Object-Relational Mapping): 데이터베이스 시스템과 데이터 모델 클래스 연결
- 관리자 화면 자동으로 구성됨
- 자체 템플릿 시스템: 화면 디자인과 로직에 대한 코딩 독립적으로 개발 진행 가능
- 캐시 시스템
- 소스 변경사항 자동 반영

<br>

### **MVT(Model View Template) 패턴(장고)**

- **Model**: DB(사용될 데이터에 대한 정의를 담고 있는 장고의 **클래스**)
- **View**: function
- **Template**: 데이터를 가지고 있는 HTML로 구성(유저들한테 보여지는 UI)

<br>

- **패턴**
  - 클라이언트로부터 요청받으면 URL분석(`URL.conf`)
  - URL 분석결과를 통해 해당 URL에 대한 처리를 담당할 **view** 결정
  - view는 자신의 로직을 실행하면서 **model**을 통해 처리하고 결과 반환
  - view는 로직 처리가 끝나면 **Template**을 사용하여 클라이언트에 전송할 HTML 생성
  - view는 최종 결과로 HTML파일을 클라이언트에 보냄

<br>

### **MVT 코딩 순서**
1. **프로젝트 뼈대** 만들기
2. **model** 코딩
3. **URLconf** 코딩하기
4. **Template** 코딩하기
5. **View** 코딩

<br>

---

<br>

### **Django 실습**

<br>

1. **프로젝트 뼈대** 만들기
  - 프로젝트: 웹 사이트의 전체 프로그램
  - 프로젝트와 앱에 필요한 **디렉토리와 파일** 생성
  - **프로젝트 생성**
    - `django-admin startproject mysite`: mysite라는 프로젝트 생성
    - `move mysite projectsite`: 프로젝트 이름 변경(mysite안에 mysite 폴더가 있기 때문에)

  - **애플리케이션 생성**
    - 애플리케이션: 모듈화된 단위 프로그램(코딩할 대상)
    - `python manage.py startapp polls`: 'polls'라는 앱 생성
    - `c:\Mytest\projectsite>` 에서 해야 함(`cd projectsite` 사용)

  - **프로젝트 설정 파일 변경**
    - `notepad settings.py`: 설정 파일 확인 및 수정
      - projectsite > mysite > settings.py 수정
      - `ALLOWED_HOSTS = []`(기본값): 모두 허용(실무에서는 ip 설정, 내 PC는 localhost)
      - `ALLOWED_HOSTS = ['192.168.35.61', 'localhost', '127.0.0.1]`
      - `INSTALLED_APP = [ ~, polls.apps.PollsConfig]` 추가(애플리케이션들을 설정파일에 등록)
      - `TIME_ZONE = Asia/Seoul` 추가
      - 프로젝트에 사용할 데이터베이스 엔진: SQLite3(기본값)

  - **기본 테이블 생성**
    - `python manage.py migrate`: 데이터베이스에 기본 테이블 생성, 데이터베이스에 변경사항이 있을 때 반영해주는 명령
      - mysite말고 projectsite에서 해야함

  - **작업 확인하기**
    - `python manage.py runserver`: 현재까지 작업 개발용 웹 서버로 확인
    - runserver 용으로 별도의 cmd창을 열어서 하는게 편리함
    - 위의 과정 실행 후 브라우저 URL에 'http://127.0.0.1:8000' 들어가보기

  - **admin 사이트 접속**
    - 'http://127.0.0.1:8000/admin'
    - admin 사이트에 로그인하기 위한 **관리자(슈퍼유저)** 생성
      - `python manage.py createsuperuser`
    - 설정한 username과 password로 **로그인** 해보기
  
  - **골격 생성**
    - `tree /F projectsite`
    - 프로젝트 폴더의 상위 폴더에서(`cd ..`)

<br>

2. **model** 코딩
  > 모델: 사용될 데이터에 대한 정의를 담고 있는 장고의 클래스  
  > ORM기법으로 애플리케이션에서 사용할 DB를 클래스로 매핑해서 코딩

  - 데이터베이스에 테이블을 생성하는 작업
  - `notepad models.py`: 테이블 정의
    - `models.py`에 정의해야함
    - polls 애플리케이션은 Question과 Choice 두 개의 테이블이 필요  
    - 예시
  ```python
  from django.db import models
  ```
  ```python
  class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

    def __str__(self):
        return self.question_text


  class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    def __str__(self):
        return self.choice_text
  ```
  ```js
  // 제약조건
  CREATE TABLE myapp_person {
    "id" seial NOT NULL PRIMARY KEY,
    "first_name" varchar(30) NOT NULL,
    "last_name" varchar(30), NOT NULL
  };
  ```
  - `notepad admins.py`: 정의된 테이블이 Admin화면에 보이게 함
  ```python
  from django.contrib import admin
  from polls.models import Question, Choice
  ```
  ```python
  admin.site.register(Question)
  admin.site.register(Choice)
  ```
  - `python manage.py makemigrations`: 데이터베이스에 변경이 필요한 사항이 있으면 실제로 반영해주는 작업
    - 상위폴더(projectsite)로 가야함
    - polls/migrations 디렉토리 하위에 migration 파일들이 생김
  - `python manage.py migrate`: 데이터베이스에 변경사항 반영
  - `python manage.py runserver`
  - 'http://127.0.0.1:8000/admin/'에서 Question, Choice 추가한 후 'http://127.0.0.1:8000/polls'에서 확인

<br>

3. **URLconf** 코딩하기
  - 파이썬의 URL 정의 방식은 자바나 PHP계열의 URL보다 직관적이고 이해하기 쉬음(Elegant URL)
  - `urls.py`(project와 app의 파일 둘 다) 파일에 URL과 처리 함수(view)를 매핑하는 파이썬 코드 작성
  ```python
  from django.urls import path
  from . import views, include
  ```

  - projectsite\mysite 
  ```python
  urlpatterns = [
    path("admin/", admin.site.urls),
    path('polls/', include('polls.urls')),
  ]
  ```
  - projectsite\polls
  ```python
  app_name = 'polls'
  urlpatterns = [
    path('', views.index, name='index'),      # /polls/
    path('<int:question_id>/', views.detail, name='detail'),       # /polls/5/
    path('<int:question_id>/results/', views.results, name='results'),     # /polls/5/results/
    path('<int:question_id>/vote/', views.vote, name='vote'),      # /polls/5/vote/
  ]
  ```

  - **처리 흐름 설계**(뷰함수와 템플릿은 서로에게 영향을 미치기 때문에 보통 같이 작업)
    - `urls.py` 작성(URLconf 내용 코딩)
    - `views.index()`함수 작성 + `index.html`
    - `views.detail()`함수 작성 + `detail.html`
    - `views.vote()`함수 작성(리다이렉션 처리)
    - `views.results()`함수 작성 + `results.html`


<br>

4. **Template** 코딩하기
  - `template/ * .html`  
  - `index.html`(기본): 최근에 실시하고 있는 질문의 리스트
  - `detail.html`: 하나의 질문에 투표할 수 있도록 답변 항목 폼으로 보여줌
  - `results.html`: 질문에 따른 투표 결과

  <br>

5. **View** 코딩
  - `views.py`
  ```python
  from django.shortcuts import get_object_or_404, render
  from django.http import HttpResponseRedirect
  from django.urls import reverse

  from polls.models import Choice, Question


  def index(request):
    # code
    return render(request, 'polls/index.html', context)

  def detail(request, question_id):
    # code

  def results(request, question_id):
    # code

  def vote(request, question_id):
    # code
  ```