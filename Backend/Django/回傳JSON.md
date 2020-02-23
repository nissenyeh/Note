# Django 要如何回傳JSON原始物件/陣列/物件？


# JSON 資料庫物件

- `serializers` 可以直接把資料庫來的物件轉成JSON

```py
from django.core import serializers
from django.http import HttpResponse, JsonResponse
from course.models import Staff, ClassRecord, Class, Course

def staff(request):
    res = serializers.serialize("json", Staff.objects.all()) 
    return HttpResponse(res)
```



# JSON 陣列

需求：資料庫中有許多員工的資料，包含員工編號、名稱、職稱、到職日...等資料，現在想要回傳只有「名稱」的JSON陣列

```js
['員工1','員工2','員工3','員工4','員工5']
```

## 設定models

模型長這樣，基本不去改動他

```py
class Staff(models.Model):
    sid = models.CharField(primary_key=True, max_length=5)
    name = models.CharField(max_length=10)
    gender = models.CharField(max_length=1)
    team = models.CharField(max_length=3)
    position = models.IntegerField()
    title = models.CharField(max_length=20, blank=True, null=True)
    birthday = models.DateTimeField(blank=True, null=True)
    onboard = models.DateTimeField()

    class Meta:
        managed = False
        db_table = 'staff'
```

## 設定urls

- 利用 `views.名稱ViewSet.as_view()`去把action進行對應

```py
from django.contrib import admin
from django.urls import include, path
from rest_framework import renderers
from course import views

staff_list = views.StaffViewSet.as_view({
    'get': 'list' #設定對應action
},renderer_classes=[renderers.StaticHTMLRenderer]) #加這個才能轉編碼

urlpatterns = [
    path('staff/',staff_list,name="staff_list"), #設定對應的action
    path('admin/', admin.site.urls),
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework'))
]
```

## 設定views

- 使用`Staff.objects.values('name')`去是name的欄位抓出來
- 使用dump把陣列轉乘JSON

```js
// 範例
AppDef.objects.values()
[{'creator': u'admin', 'apptype_name': u'uc3g', 'apptype_chn_name': u'3G\u95e8\u6237', 'note': u'', ...},...]

AppDef.objects.values('apptype_name')
[{'apptype_name': u'uc3g'},...]
```

```py
from django.http import HttpResponse, JsonResponse
from course.models import Staff, ClassRecord, Class, Course


def staff(request):
    queryset = Staff.objects.values('name')
    result = []
    for i in queryset:
        result.append(i['name'])
    res = json.dumps(result,ensure_ascii=False)

    return HttpResponse(res)
```

# JSON物件


## url

```py
urlpatterns = [
    path('', cousre.index),
    path('course_detail/<name>', cousre.courseDetail),
]
```

## views

```py
def courseDetail(request, name):

    staff =  Staff.objects.get(name=name)
    records = ClassRecord.objects.filter(s_id=staff.sid)
    
    res = []
    for classrecord in records:
        course = {
            'name':classrecord.c.cid.name,
            'teacher':classrecord.c.teacher.name,
            'start':classrecord.c.start.strftime("%Y-%m-%d %H:%M:%S"),
            'end':classrecord.c.end.strftime("%Y-%m-%d %H:%M:%S"),
            'isapplied':classrecord.isapplied,
            'isattended':classrecord.isattended
        }
        res.append(course)

    res = json.dumps(res,ensure_ascii=False)
    return HttpResponse(res)
```