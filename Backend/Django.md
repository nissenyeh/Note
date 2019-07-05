	
[English Note](#Django)  / [Chinese Note](#Django介紹) 


# Django


### How Django deal request?

1. User types the url and keypress, the request is created
2. The request will be sent to 'urls.py'
3. Django will match the url `with urlpatterns` data
4. If the match happend, Django will return the view.

```py
#urls.py
    from app import views
    from django.urls import path
    urlpatterns = [
      path('index/', views.index, name='index'),
    ]
```

```py
#views.py
def index(request):
    ...
    return render(request,'index.html')
```


# Virtual Environment

## What's Virtual Environment

- A Virtual Environment which can run python.The pip packages is installed in different environment won't disturb each others.

## How to install Virtual Environment

- Create a random file
- create a Virtual Environment 
```vim
python3 -m venv djangogirls_venv // 
```

- swithch to the Virtual Environment 
```vim
source djangogirls_venv/bin/activate 
```

# Run Django 

- How Django connect to Database?
- Database setting in `.env` file

```py
DB_CONNECTIONS=mysql
DB_HOST=XXX.XXX.X.XXX
DB_PORT=XXXX
DB_DATABASE=maltose-dev
DB_USERNAME=root
DB_PASSWORD=password
```

- Install package which project need

```js
$ source djangogirls_venv/bin/activate 
$ pip install XXXX or
$ pip install -r `requirements/local.txt` 
```

- Run Server
```js
$ python manage.py runserver
```


# Connect to MySQL



------------------------------------

# Django介紹

### Django 如何處理請求？
1. 用戶在敲下你的網址並回車，生成請求;
2. 請求傳遞到urls.py;
3. Django的去urlpatterns的中匹配鏈接（Django的會在匹配到的第一個就停下來）;
4. 一旦匹配成功，則Django便會給出相應的視圖頁面（該頁面可以為一個的Python的函數，或者基於視圖（Django的內置的）的類），也就是用戶看到的頁面;

```py
#urls.py
    from app import views
    from django.urls import path
    urlpatterns = [
      path('index/', views.index, name='index'),
    ]
```

```py
#views.py
def index(request):
    ...
    return render(request,'index.html')
```

# 虛擬環境

## 什麼是虛擬環境

- 一個可以 Run python 的虛擬環境，可以在裡面安裝各種套件，然後不同虛擬環境不會互相影響.

## 如何安裝虛擬環境

- 建造一個隨便的檔案
- 建造一個虛擬環境
```vim
python3 -m venv djangogirls_venv // 
```

- 切換虛擬環境
```vim
source djangogirls_venv/bin/activate 
```

# 啟用Django並連接資料庫

- 設定 `.env` 檔案

```py
DB_CONNECTIONS=mysql
DB_HOST=XXX.XXX.X.XXX
DB_PORT=XXXX
DB_DATABASE=maltose-dev
DB_USERNAME=root
DB_PASSWORD=password
```

- 在虛擬環境中安裝套件

```js
$ source djangogirls_venv/bin/activate 
$ pip install XXXX or
$ pip install -r `requirements/local.txt` 
```

- 啟用Django
```js
$ python manage.py runserver
```

# 連接資料庫