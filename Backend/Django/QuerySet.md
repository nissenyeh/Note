
# QuerySet


### QuerySet 是什麼？ objects.all() 和 objects.get() 和 objects.filter()

- QuerySet是Django的一種資料結構，本質是list，但是提供許多自定義的方法，必須用for迴圈把資料拿出來用

```python
Post.objects.all() #可以將所有的物件都列出來
<QuerySet [<Post: my post title>, <Post: another post title>, <Post: Sample title>]>

Post.objects.filter(age='10') #可以把欄位age=10的所有資料列出來
```

以下方式只會得到「唯一筆資料」
```python
Post.objects.get(name='小明') #可以把欄位name=小明的「唯一筆」資料列出來

 <p>{{person.name}}<p>
```


- `get`：返回符合條件的唯一一筆資料。（注意：如果找不到符合條件的資料、或是有多筆資料符合條件，都會產生 exception）
- `filter`：返回符合條件的陣列。如果找不到任何資料則會返回空陣列。

### 常用方法

code           | 作用  | SQL對應 | 
--------------|:-----:|:-----:|
Database.objects.get(pk=1)    | 找到第pk筆資料 | | 
Database.objects.all()   | 顯示所有資料 | SELECT ＊ FROM "schema"| 
Database.objects.filter(title__contains='Trip')| 搜尋特定條件的資料| select * from “schema” where title like 'trip'; | 
Database.objects.values('name')   | 搜索特定欄位，會回傳一個像 [{'name':'名字1'},{'name':'名字2'}]的list | select name from “schema” | 
Database.objects.create(title='First Cup') | 建立資料 | | 
Database.objects.distinct()   | 去除重複 |select distinct(*) from “schema”  | 

- __contain 在乎大小寫：Database.objects.filter(name__contains="e") 
- __icontains 不在乎大小寫：Database.objects.filter(name__icontains="e") 


