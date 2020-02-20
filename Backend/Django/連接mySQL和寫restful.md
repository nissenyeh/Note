# Django 和 MySQL的連接並且撰寫Restful API

# 設定讓Django 和 MySQL連線

- 安裝`PyMySQL`（一種Python3.x 版本中用於連接MySQL的庫）

```py
pip3 install PyMySQL
django-admin startproject project_name #開啟專案
python manage.py startapp app_name #開啟APP
```
- 設定`__init__.py`讓PyMySQL替代MySQLdb（在原始的那個資料夾，不是app的那個）

```py
import pymysql
pymysql.install_as_MySQLdb()
```

- 在`settings.py`設定database

```
DATABASES = {
    ‘default’: {
    ‘ENGINE’: ‘django.db.backends.mysql’,
    ‘NAME’: ‘mydatabase’, #schema名稱
    ‘USER’: ‘root’,
    ‘PASSWORD’: ‘2xuixlji’,
    ‘HOST’: ‘localhost’,
    ‘PORT’: ‘3306’,
    }
}
```

- 把MySQL的表格還原回成Django model

```py
python3 manage.py inspectdb
or
python3 manage.py inspectdb > APP資料夾/models.py  
```

> 如果出現問題參考這篇 https://stackoverflow.com/questions/55657752/django-installing-mysqlclient-error-mysqlclient-1-3-13-or-newer-is-required


### 將MySQL資料顯示到Admin後台

- 設定超級使用者，讓自己可以登入到Admin

```py
python3 manage.py createsuperuser
```

- 記得註冊APP，確保APP的資料有被啟用

```py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp' #app名稱
]
```

- 在`admin.py`中註冊模型，讓後台可以顯示mySQL的資料

admin.py
```py
from django.contrib import admin
# Register your models here.
from .models import Table # 引入模型

class Firstdataappadmin(admin.ModelAdmin):
    list_display=('id','title','comment_count','like_count','createdat','school','content') # 欄位

admin.site.register(Table,Firstdataappadmin)  # 註冊模型
```

### Model的刪改

- 把model改動的東西改回

```py
python3 manage.py makemigrations #記錄下你所有的關於models.py的改動
python3 manage.py migrate # 將該改動作用到數據庫，比如產生table之類
```

# 撰寫Restful API

## REST framework

- REST提供viewsets,ModelsSerializer方便的建構API
- Model：跟資料庫溝通
- Serialization：把Model的資料序列化，讓View可以用（Model跟View的溝通橋樑）
- View：處理CRUD，看URL過來的方法是什麼(POST,GET...etc)，就把回覆傳回去

## install

- 安裝`djangorestframework`

```
pip3 install djangorestframework

```

- 在settings裡面，啟用`rest_framework`，並且設定Pagination，可以設定一頁回傳多少data

```py
INSTALLED_APPS = [
    ...
    'rest_framework', # 啟用rest_framework
]

REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination', # 設定Pagination
    'PAGE_SIZE': 10    # 一頁 return 多少資料
}
```

## 加上serializers

- 在App下面增加`serializers.py`，把model的資料轉成JSON


### 什麼是serializers？

serializers是一個用來把queryset（Django中的一種資料結構，本質是一個list）轉變成JSON純文字

```py
from rest_framework import serializers
from rest_framework.renderers import JSONRenderer

class Comment(object):  #這是一個純粹的Object
    def __init__(self, email, content, created=None):
        self.email = email
        self.content = content
        self.created = created

comment = Comment(email='leila@example.com', content='foo bar') #這是一個純粹的Object

print(comment) #印出<course.serializers.Comment object at 0x106e823c8>

class CommentSerializer(serializers.Serializer): #這是一個Serializer
    email = serializers.EmailField()
    content = serializers.CharField(max_length=200)
    created = serializers.DateTimeField()

serializer = CommentSerializer(comment) #把物件丟到，Serializer中
print(serializer.data) #把物件丟到，Serializer中，印出{'email': 'leila@example.com', 'content': 'foo bar', 'created': None}

json = JSONRenderer().render(serializer.data)
print(json) #用JSONRenderer().render，最後可以印出'{"email":"leila@example.com","content":"foo bar","created":null}'

```

### 如何使用？

serializers.py是專門把Model複雜的數據結構，轉換成JSON或是XML之類的其他格式

```py
{
  url:...,
  username:...,
  email:...,
  groups:...,
}
```

如果想要這樣的JSON就可以這樣寫

```py
from app專案.models import User, Group
from rest_framework import serializers


class 名稱Serializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = User
        fields = ['url', 'username', 'email', 'groups']
```

## 加上Views
- 在App下面寫views，讓url引發對應指令
- `fields`當中可以設定JSON格式有哪些屬性。
> 參考[文件](https://www.django-rest-framework.org/tutorial/3-class-based-views/)

```py
from app專案.models import User
from rest_framework import viewsets
from tutorial.quickstart.serializers import UserSerializer


class 名稱ViewSet(viewsets.ModelViewSet):
    """
    API endpoint that allows users to be viewed or edited.
    """
    queryset = User.objects.all()
    serializer_class = UserSerializer
```

- 在Project下面寫urls.py

```py
from django.urls import include, path
from rest_framework import routers
from tutorial.quickstart import views

router = routers.DefaultRouter()
router.register(r'users', views.UserViewSet)

# Wire up our API using automatic URL routing.
# Additionally, we include login URLs for the browsable API.
urlpatterns = [
    path('', include(router.urls)), #要有這行
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework'))
]
```