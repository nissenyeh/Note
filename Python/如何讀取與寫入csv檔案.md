
# CSV檔案的read與write

## 檔案的讀取

希望可以把該筆資料根據「斷行」輸出到陣列中
```
Nissen,Tim
Jean,Jane
Kevin,Jeffery
David,Fen
```
希望可以輸出為以下，可以使用 `file.readlines()`

```js
['Nissen,Tim', 'Jean,Jane', 'Kevin,Jeffery', 'David,Fen']
```

或是以下可以使用 `csv.reader(file) `

```js
[['Nissen','Tim'], ['Jean','Jane'], ['Kevin','Jeffery'], ['David','Fen']]
```

可以使用以下函式

## file.readlines() 輸出陣列


- `file.readlines()`：會把csv的每一行當成元素丟入陣列

```py
exp=[]
with open('exp.txt', 'r') as file:
    for data in file.readlines():
        data = data.strip() #strip()會去掉空白，或換行符號\n
        exp.append(data)

print(exp)
```

```js
['Nissen,Tim', 'Jean,Jane', 'Kevin,Jeffery', 'David,Fen']
```


### csv.reader(file) 輸出二維陣列

- `csv.reader(file)`：會把csv檔案轉換成一個「二維陣列」的物件

執行以下程式碼

```py
with open('exp.txt', 'r') as csvfile:
    print(list(csv.reader(csvfile)))
```

會輸出

```js
[['Nissen', 'Tim'], ['Jean', 'Jane'], ['Kevin', 'Jeffery'], ['David', 'Fen']]
```

## file.read() 輸出字串

- file.read()：會把csv統一輸出為「一個字串」

```py
with open('exp.txt', 'r') as file:
    print(file.read())
```

會輸出一個字串（以下全部都在同一個字串中）
```js
Nissen,Tim
Jean,Jane
Kevin,Jeffery
David,Fen
```

## 檔案的寫入

希望可以在csv檔案輸出為：

```js
1,2,3
```

## 使用csv.writer 寫入陣列

- csv.writer(file,delimiter) 
- writer.writerow(陣列) 

```py
import csv
with open('exp.txt', 'w') as file:  # w 會直接覆寫, a會在文件後面加上文字
    writer = csv.writer(file, delimiter=',') 
    writer.writerow([1,2,3]) 
```

```py
1,2,3
```

> 如果 delimiter 如果是 ' ' 就會輸出 1 2 3




## 其他問題

with open(file, newline='') 的newline=''到底在幹嘛...


