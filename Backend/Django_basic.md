# Django:Model, View , Serialization


推薦資源：[Django Girls 學習指南](https://djangogirlstaipei.gitbooks.io/django-girls-taipei-tutorial/django/models.html)

## REST framework

- REST提供viewsets,ModelsSerializer方便的建構API

- Model：跟資料庫溝通
- Serialization：把Model的資料序列化，讓View可以用（Model跟View的溝通橋樑）
- View：處理CRUD，看URL過來的方法是什麼(POST,GET...etc)，就把回覆傳回去

## Model: 不用寫討厭的SQL就可以控制你的資料庫

- 在model當中可以定義資料庫當中有什麼欄位


``` py
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField(blank=True)
    photo = models.URLField(blank=True)
    location = models.CharField(max_length=100)
    created_at = models.DateTimeField(auto_now_add=True)
  
  class Meta:
    db_table = "my_post" //自訂資料庫中的table名稱
```
> 可以不需要meta屬性


### Migration

- 當model改完後，就可進行migration，讓Django幫忙把語言轉成SQL，再讓SQL去更改資料庫


```py
python manage.py makemigrations
```
- 把model的語法轉成mySQL並且去改變database
```py
python manage.py migrate
```


## Serializers：把Model變成JSON囉！（Model跟View的溝通橋樑）

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



## Views：當URL被分過來，看是POST/GET然後去跟MODEL找資料！



- REST 提供ModelViewSet類別，只要要給他`queryset` 跟`serializer_class`，就可以享用CRUD的功能
- 提供.list(), .retrieve(), .create(), .update(), .partial_update(), and .destroy()
>  ModelViewSet繼承自GenericAPIView，GenericAPIView則繼承自View（Django的class)

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