
# Python與Django課程

- 推薦資源：[Django Girls 學習指南](https://djangogirlstaipei.gitbooks.io/django-girls-taipei-tutorial/django/models.html)
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

- 利用startproject啟動一個專案，產生重要的manage.py以及setting等重要的設定檔案

```shell
django-admin startproject <<專案名稱>>
```

> 利用把「參數」 傳到manage.py 的方式來操作程式

- 利用startapp創建一個app專案本身（剛剛只有設定檔案）

```
python3 manage.py startapp <<App名稱>>
```

- 啟用伺服器

```
python3 manage.py runserver
```

## 套件

- `contrib`：各種小工具的包，包含admin/auth/redirects/sessions/sites


# 1. Model: 與資料庫聯繫

<!-- model  -->

在使用Django的時候，不需要直接寫SQL指令，而是可以透過Model設定class（相當於資料庫的一個table），寫完後，再讓Django去產生一個中介檔案，然後去操作資料庫。

1. 去model檔案（在app下面），把表格的欄位設定好。例如

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

> 可以不需要meta屬性

當model改完後，就可進行migration，讓Django幫忙把語言轉成SQL，再讓SQL去更改資料庫

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


# 2. View: 提供網站回應，當URL被分過來，View再根據是POST/GET然後去跟MODEL

- Url會和view設定再一起，當相關的url被觸發時，就會觸動來自view的函式
- REST 提供ModelViewSet類別，只要要給他`queryset` 跟`serializer_class`，就可以享用CRUD的功能
- 提供.list(), .retrieve(), .create(), .update(), .partial_update(), and .destroy()
>  ModelViewSet繼承自GenericAPIView，GenericAPIView則繼承自View（Django的class)



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


Restapi的寫法
```py
# Create your views here.
from musics.models import Music
from musics.serializers import MusicSerializer
from rest_framework import viewsets

# Create your views here.
class MusicViewSet(viewsets.ModelViewSet):
    queryset = Music.objects.all()
    serializer_class = MusicSerializer
```


- `get`：返回符合條件的唯一一筆資料。（注意：如果找不到符合條件的資料、或是有多筆資料符合條件，都會產生 exception）
- `filter`：返回符合條件的陣列。如果找不到任何資料則會返回空陣列。


code           | 作用  | 
--------------|:-----:|
Database.objects.get(pk=1)    | 找到第pk筆資料 | 
Database.objects.all()   | 顯示所有資料 | 
Database.objects.create(title='First Cup') | 建立資料 | 
Database.objects.filter(title__contains='Trip')| 搜尋資料| 
Database.objects.distinct()   | 去重複 | 

- __contain 在乎大小寫：Database.objects.filter(name__contains="e") 
- __icontains 不在乎大小寫：Database.objects.filter(name__icontains="e") 

- querySet.distinct() 去重複

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

## 模板的 include ＆ extend

- 不同的template之間可以使用include來「引用」，用extend 「繼承」


```html
<!-- base.html -->
<!DOCTYPE html>
<html>
    <head>
    <meta charset='utf-8'>
    <title>
        {% block title %} {% endblock %}
    </title>
    </head>
    <body>
        {% comment %} {% include 'header.html' %} {% endcomment %}
        {% block headmessage %} {% endblock %}  # 預期這裡要塞叫headmessage的東西進來
        <hr>
        {% block content %} {% endblock %}   # 預期這裡要塞叫content的東西進來
        <hr>
        {% include 'footer.html' %}  # 引用別的模板得所有內容
    </body>
</html>
```

```html
<!-- index.html -->
{% extends 'base.html' %}  #繼承base.html的內容
{% block title %} 歡迎光臨我的部落格 {% endblock %}  
{% block headmessage %} 
<h3 style='font-family:標楷體;'>本站文章列表</h3>
{% endblock %}
{% block content %}  #會把資料塞到base中的{% block content %}區域
    {% for post in posts %}
        <p>
            <a href='/post/{{post.slug}}'>{{ post.title }}</a>
        </p>
    {% endfor %}
{% endblock %}
```

## 設定靜態資料夾 static

- 在根目錄下manage.py那一層新增一個`static`資料夾，用來把圖片放進去


```py
STATIC_URL = '/static/'
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]  #告訴它static在哪裡
```


# 4.Serializers：把Model變成JSON囉！（Model跟View的溝通橋樑）

- 專門把Model複雜的數據結構轉換成JSON或是XML之類的其他格式

```py
{
  id:...,
  song:...,
  singer:...,
  last_modify_data:...,
  created:...
}
```
如果想要這樣的JSON就可以這樣寫

```py

from rest_framework import serializers
from musics.models import Music

class MusicSerializer(serializers.ModelSerializer):
    class Meta:
        model = Music
        fields = ('id', 'song', 'singer', 'last_modify_date', 'created')
```

- `model`當中可以指定是哪個模組要序列化
- `fields`當中可以設定JSON格式有哪些屬性。


### 複雜的JSON格式

```py
class CaseSerializer(serializers.ModelSerializer):
    disease = DiseaseNameSerializer()
    test_disease = DiseaseNameSerializer()
    symptoms = serializers.SerializerMethodField()
    PEs = serializers.SerializerMethodField()
    RFs = serializers.SerializerMethodField()
```
- SerializerMethodField() = get_XXX
```py
  def get_symptoms(self, obj):
      locale = self.context['request'].query_params.get('locale', 'zh_cn')
      queryset = Case.objects.symptoms(pk=obj.id, locale=locale)
      print(Case.objects)
      return queryset
```

#### Shell

`python manage.py shell`

```py
from apps.data-mangers.models import Sand.Case
Sand.objects.all() // 可以看到Sand class有的所有的物件
Sand.object.filter(id=666),values('sand_diseases')  // 可以看到sand_diseases數值
sand.object.create(disease_id=7,case_id=666) //創建資料
```

#### ManyToMany 欄位

- 一個欄位如果是`manyTomany`可以用ManyToManyField去寫，然後透過一個`中介`的model去連到另一個

```py
class Case(models.Model):
  sand_diseases = models.ManyToManyField(DiseaseMaster, related_name='sands', through="Sand")

  class Meta:
      db_table = "case"


class Sand(models.Model):
    disease = models.ForeignKey(DiseaseMaster, on_delete=models.CASCADE)
    case = models.ForeignKey(Case, related_name='sands', on_delete=models.CASCADE)

    class Meta:
        db_table = "case_sand"


class DiseaseMaster(models.Model):
    master_dis_id = models.PositiveIntegerField(primary_key=True)
    term_name = models.CharField(max_length=255, db_index=True)
    status = models.PositiveIntegerField()
    icd10 = models.CharField(max_length=255, null=True, db_index=True)
    source = models.CharField(max_length=255)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    objects = DiseaseMasterManager()

    class Meta:
        db_table = "disease_master"
```

- 在中介的model新增資料

```
import Sand from apps.....
Sand.objects.create(master_dis_id=1, case_id=2) 
```