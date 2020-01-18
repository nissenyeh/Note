# Django 和 MySQL的連接


# 安裝與設定
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



# 常見的mySQL和Django聯繫

- 把MySQL的ER model還原回成model

```py
python3 manage.py inspectdb
or
python3 manage.py inspectdb > APP資料夾/models.py  
```

如果出現問題參考這篇 https://stackoverflow.com/questions/55657752/django-installing-mysqlclient-error-mysqlclient-1-3-13-or-newer-is-required

- 把model改動的東西改回

```py
python3 manage.py makemigrations #記錄下你所有的關於models.py的改動
python3 manage.py migrate # 將該改動作用到數據庫，比如產生table之類
```

python3 manage.py createsuperuser