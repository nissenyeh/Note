# Django 和 MySQL的連接


# 設定讓Django 和 MySQL連線

- 安裝`PyMySQL`（一種Python3.x 版本中用於連接MySQL的庫）

```py
pip3 install PyMySQL
django-admin startproject project_name #開啟專案
python manage.py startapp app_name #開啟APP
```
- 設定`__init__.py`讓PyMySQL替代MySQLdb

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
