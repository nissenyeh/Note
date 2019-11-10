
# Python與Django課程

- 網址：http://homepage.ntu.edu.tw/~jfanc/Django.html?clsp=321
- 密碼：wdp321ers

## 介紹

- Django是一個MVT的結構，可以利用很短的時間幫助工程師建立一個完整的網站（比Flask完整）
 - M（model）：主要用來操作資料庫，可以建立表格等等
 - V（view)：當網址被觸發時，就會觸發來自view的函式（回傳html或是任何函式）
 - T（template）：當回傳html的結果前，view可以去把資料丟進去template續染，然後再回傳。


## 啟用Django網站

- 安裝Django

```shell
pip3 install Django
```

- 開啟專案，然後會出現重要的manage.py以及setting檔案。

```shell
django-admin startproject <<專案名稱>>
```

> 利用把「參數」 傳到manage.py 的方式來操作程式

- 創業APP（利用 manage.py 這隻檔案去創建APP）

```
python3 manage.py startapp <<App名稱>>
```

- 啟用伺服器

```
python3 manage.py runserver
```


# 1. Model: 與資料庫聯繫

<!-- model  -->

在使用Django的時候，不需要直接寫SQL指令，而是可以透過Model設定class（相當於資料庫的一個table），寫完後，再讓Django去產生一個中介檔案，然後去操作資料庫。

1. 去model檔案，把表格的欄位設定好。例如

- class Post 是 「設定一個名為Post的table」
- title = models.CharField(max_length=200) 是 「設定一個格式為char的 title的欄位」
- pub_date = models.DateTimeField是 「設定一個格式為date的title的欄位」


```py
class Post(models.Model):
    title = models.CharField(max_length=200)
    slug = models.CharField(max_length=200)
    body = models.TextField()
    pub_date = models.DateTimeField(default=timezone.now)

    class Meta:
        ordering = ('-pub_date',)

    def __unicode__(self):
        return self.title

    def __str__(self):
        return self.title
```

2. `python3 manage.py makemigration` 建立中介檔案（操作資料庫的指令檔案）
3. `python3 manage.py migrate` 把中介檔案去真的寫入資料庫


#### 補充：__str__ 是什麼？

是當class被實體化的時候，print（實體）就會印出__str__ 中 retrun 的文字


```py
class Hello(models.Model):

    def __str__(self):
        return 'hello'

hi = Hello()
print(hi)  # 印出 hello
```

### 建立管理員

```py
python manage.py createsuperuser
```

```py
from django.contrib import admin

# Register your models here.
from .models import Post

class muticolumn(admin.ModelAdmin):
    list_display = ('title','slug','pub_date')

admin.site.register(Post,muticolumn)


```

# 2. View: 提供網站回應

- Url會和view設定再一起，當相關的url被觸發時，就會觸動來自view的函式

## 設定Url路徑 

```py 
urlpatterns = [
    path('admin/', admin.site.urls),
    path('',homepage) #當根目錄被觸發時，就會啟用homepage的函式
]

```

## 設定view的函式

- 在以下例子中，如果根目錄被觸發就會啟用homepage的函式，並起回復HttpResponse(html)

```py 
from django.shortcuts import render
from django.template.loader import get_template
from django.http import HttpResponse
from .models import Post
from datetime import datetime

def homepage(request):
    template = get_template('index.html')
    posts = Post.objects.all()
    now = datetime.now()
    html = template.render(locals()) #把區域變數放進去，然後渲染樣板
    return HttpResponse(html)
```
> local可以把所有的「區域變數」抓出來

### QuerySet 是什麼？  objects.all()和objects.get()和objects.filter()

以下方式會得到QuerySet，必須用for迴圈把資料拿出來用

```python
Post.objects.all() #可以將所有的物件都列出來
<QuerySet [<Post: my post title>, <Post: another post title>, <Post: Sample title>]>

Post.objects.filter(age='10') #可以把欄位age=10的所有資料列出來

{% for person in persons %}
    <p>{{person.name}}<p> #需要for迴圈把資料拿出來（即使QuerySet只有一筆資料）
{% endfor %}
```

以下方式只會得到「唯一筆資料」
```python
Post.objects.get(name='小明') #可以把欄位name=小明的「唯一筆」資料列出來

 <p>{{person.name}}<p>
```



# 3. Template：提供好看的html樣板

- 在專案的根目錄建立一個template的資料夾，放index.html進去
- 在template中可以寫python的語法，然後Django會把檔案渲染後，然後在把編譯好的html丟出去。

```html
<html>
    <head>
    <meta charset="utf-8">
    <title>歡迎來到我的部落格</title>
    </head>
    <body>
        <h1> 歡迎來到我的部落格 </h1>
        <hr>
        {% for post in posts %}
        <!-- 開始for迴圈 -->
        <p style='font-family: 微軟正黑體;font-size:16pt;font-weight:bold;'>
            {{ post.title }}
            <!-- 印出變數 -->
        </p>
        <p style='font-family: 微軟正黑體;font-size:10pt;letter-spacing:1pt;'>
            {{ post.body }}
        </p>
        {% endfor %} 
        <!-- endfor 表示for迴圈結束 -->
        <hr>
        <h3>現在時間:{{ now} }</h3>
    </body>
</html>
```
