## To-do list 실습

- 화면 설계
  - 입력
  - 출력
  - 기능

- 데이터 설계(DB 모델링)
- 데이터 식별,도출(저장, 사용)
- 테이블 필드명, 필드 타입, 필드길이
  - To do content: CharField(255)
  - isDone: BooleanField()

<br>

---

<br>

1. **프로젝트 뼈대** 만들기
  - `django-admin startproject ToDoList`
  - `python manage.py startapp my_to_do_app`(\ToDoList)
  - `notepad settings.py`(\ToDoList\ToDoList)
  ```python
  INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "my_to_do_app",  # 추가
  ]
  ```
  ```python
  TIME_ZONE = "Asia/Seoul"
  ```

  - `python manage.py migrate`(\ToDoList)
  - `python manage.py runserver`

  - 슈퍼유저 설정: `python manage.py createsuperuser`(\ToDoList)

<br>

2. **model 코딩**

- `\ToDoList\my_to_do_app\models.py`
```python
from django.db import models

class Todo(models.Model):
    content = models.CharField(max_length = 255)
    isDone = models.BooleanField(default=False) #완료버튼에 사용
```

- `\ToDoList\my_to_do_app\admin.py`: models.py파일에서 정의한 테이블도 admin 사이트에서 보이도록 등록
```python
from django.contrib import admin
from my_to_do_app.models import Todo
# models.py 모듈에서 정의한 ToDo클래스 임포트

admin.site.register(Todo)
# 임포트한 클래스 admin사이트에 등록
```

- `python manage.py makemigrations`(\ToDoList): my_to_do_app/migrations 디렉토리 하위에 마이그레이션 파일들이 생김
- `python manage.py migrate`: 마이그레이션 파일들을 이용해 데이터베이스에 테이블 생성

<br>

3. **URL 코딩**

- `\ToDoList\ToDoList\urls.py`
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('', include('my_to_do_app.urls')),
    path("admin/", admin.site.urls),
]
```

- ` `
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('createTodo/', views.createTodo, name='createTodo'),
    path('doneTodo/', views.doneTodo, name='doneTodo')
 ]
```

<br>

4. **View** 함수 `index()` 및 **Template** 작성

- my_to_do_app\Template\index.html 만들기
- `views.py`에 `index()`함수 정의
```python
from django.shortcuts import render
from django.http import HttpResponse, HttpResponseRedirect
from django.urls import reverse
from .models import * # models.py에서 생성된 객체 모두 import(class Todo)

def index(request):
     todos = Todo.objects.all() # Todo 클래스 이용해 db에 저장된 모든 레코드 select
     content = {'todos': todos} #content dict 생성
     return render(request, 'my_to_do_app/index.html', content) #index.html 파일로 전달
     # # return HttpResponse("my_to_do_app first page")
     # return render(request, 'my_to_do_app/index.html')
```

- `views.py`에 기능 함수 정의
```python
def createTodo(request):
     user_input_str = request.POST['todoContent']
     new_todo = Todo(content=user_input_str)
     new_todo.save()
     return HttpResponseRedirect(reverse('index'))
     # return HttpResponse("DB에 저장되었어요 =>" + user_input_str)

def doneTodo(request):
    done_todo_id = request.GET['todoNum']
    print("완료한 todo의 id",done_todo_id)
    todo = Todo.objects.get(id = done_todo_id)
    todo.isDone = True
    todo.save()
    return HttpResponseRedirect(reverse('index'))

# def deleteTodo(request):
#     done_todo_id = request.GET['todoNum']
#     print("완료한 todo의 id",done_todo_id)
#     todo = Todo.objects.get(id = done_todo_id)
#     # todo.isDone = True
#     todo.delete()
#     return HttpResponseRedirect(reverse('index'))
```

- 작업 확인: `python manage.py dbshell`
```
(base) C:\Mytest\ToDoList>python manage.py dbshell
SQLite version 3.40.1 2022-12-28 14:03:47
Enter ".help" for usage hints.
sqlite> .tables
auth_group                  django_admin_log
auth_group_permissions      django_content_type
auth_permission             django_migrations
auth_user                   django_session
auth_user_groups            my_to_do_app_todo
auth_user_user_permissions
sqlite> select * from my_to_do_app_todo;
1|오늘의 할일|1
2|내일의 할일|1
3|데이터엔지니어링|1
4|데이터사이언스|1
5|오늘의 할일|0
```

<br>

---

<br>

