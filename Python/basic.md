# Python

Python 分為2.0, 3.0版本，以下為 3.0 版本的筆記

## 基礎常用函式

### 印出資料 print()
> 在2.x可以不用括號，但在3.x中print()是函式

- `print("{} {} ".format("",""))`: 可以預設列印格式

```python
"{} {}".format("hello", "world")    # 不设置指定位置，按默认顺序
## >> 'hello world'
"{0} {1}".format("hello", "world")  # 设置指定位置
## >> 'hello world'
 
```

- `print("",end=' ')`: print預設會換行，end意味末尾不換行加空格。

``` py
for i in range(5):
  print(i,end=' ')
## 1 2 3 4 5
```

### 輸入資料 input()

- `input('')`:請使用者提供資料

```python
age = input('How old are you?')
print('I am ' + age + ' years old')
```
# 常用語法

### If ... else

python的if...else 
- 後面都要有`冒號:`
- 用空白來進行區隔

```python
age = int(input('How old are you?'))
if age >= 20:
  print('adult')
else:
  print('not adult')
```

### for ... in list

python的if...else 
- 後面都要有`冒號:`
- 用空白來進行區隔
- range(11)表示0..10
  - range(0,11)表示１..10
  - range(1,11,2) 表示 [1,3,5,7,9]

```python
for a in range(10):
  print(a)  // 1,2,3....9
```

### While

python 的 while
- 後面要有`冒號:`
- 用空白來進行區隔
- 有一點像for迴圈

```python
while age < 20:
  age = age + 1
  print(age)
```

### def 函式

- 後面要有`冒號:`
- 用空白來進行區隔

``` python
def addNum(a, b):
  return a+b
print(addNum(1,2)) // 3
```



# 基本數據類型：

- 有序資料：
  - 列表(list)：有序的元素列表
  - 元組(tuple)：有序，但不能刪改的list
- 無序資料:
  - 字典(dictionarylist)：具有key,value的物件
  - 集合(set)：只具有key的無序物件（不等於list)


## 有序資料

### 列表:[list]

- append('element'):在尾部添加元素
- pop():刪除尾部的元素
- insert(index,'element') 在index的位置插入元素
- len(列表):計算列表的長度

```python
lists = ['a','b','c']
lists.append('d')  # ['a','b','c','d']
lists.pop()  # ['a','b']
lists.insert(0,'o')  # ['o', 'a','b','c']
len(lists) # [3]
```

### 元组:(tuple)

- 跟list的差別在於tuple只能訪問，不能修改，所以沒有append(), pop(), inset()之類的方法

```python
tuples = ('tupleA','tupleB')
print(tuples[0]) // tupleA
```

## 無序資料

### 字典:{dictionary}

- 相當於JS的物件結構，具有key,value
- key一定要有''

```python
nissen = {
  'name' : 'nissen',
  'age' : 20,
}
```

- 拜訪value:
  - nissen['name']
  - nissen.get('name')
- 增加key,value: nissen['gender'] = 'female'
- 刪除key,value: nissen.pop('name')
- 查看key是否在裡面 :print('name' in nissen)

### 集合:set([set])

- set是無序的key集合，因此不能用index拜訪
- remove('a')：移除集合的元素
- add('k')：增加集合的元素
- print('a' in s):查看元素是否存在

```python
a = ['a', 'b', 'c']
s = set(['a', 'b', 'c'])

print(a[0]) # 'a'
print(s[0]) #錯誤 TypeError: 'set' object does not support indexing
```


