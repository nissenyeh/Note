
## 如何讀取csv檔案？




## csv.reader(file) 和  file.readlines(),file.read() 的差異？

假設同樣一筆資料如下
```
sepal_length,sepal_width,petal_length,petal_width,species
5.1,3.5,1.4,0.2,setosa
4.9,3,1.4,0.2,setosa
4.7,3.2,1.3,0.2,setosa
4.6,3.1,1.5,0.2,setosa
```

- csv.reader(file)：會把csv檔案轉換成一個「二維陣列」的物件

```py
with open('exp.txt', 'r') as csvfile:
    print(list(csv.reader(csvfile)))
```

會輸出

```js
[['sepal_length', 'sepal_width', 'petal_length', 'petal_width', 'species']
['5.1', '3.5', '1.4', '0.2', 'setosa']
['4.9', '3', '1.4', '0.2', 'setosa']
['4.7', '3.2', '1.3', '0.2', 'setosa']
['4.6', '3.1', '1.5', '0.2', 'setosa']]
```

- file.readlines()：會把csv的每一行當成元素丟入陣列

```py
exp=[]
with open('exp.txt', 'r') as file:
    for data in file.readlines():
        data = data.strip() #strip()會去掉空白，或換行符號\n
        exp.append(data)

print(exp)
```

```js
['sepal_length,sepal_width,petal_length,petal_width,species', '5.1,3.5,1.4,0.2,setosa', '4.9,3,1.4,0.2,setosa', '4.7,3.2,1.3,0.2,setosa', '4.6,3.1,1.5,0.2,setosa']
```

- file.read()：會把csv統一輸出為「一個字串」

```py
with open('exp.txt', 'r') as file:
    print(file.read())
```

會輸出一個字串（以下全部都在同一個字串中）
```js
sepal_length,sepal_width,petal_length,petal_width,species
5.1,3.5,1.4,0.2,setosa
4.9,3,1.4,0.2,setosa
4.7,3.2,1.3,0.2,setosa
4.6,3.1,1.5,0.2,setosa
```

## 如何用 csv.writer 寫入陣列

- csv.writer(file,delimiter) 
- writer.writerow(陣列) 

```py
import csv
with open('exp.txt', 'w') as file:  # w 會直接覆寫, a會在文件後面加上文字
    writer = csv.writer(file, delimiter=',') 
    writer.writerow([1,2,3]) 
```

```py
# 如果 delimiter 如果是' '就會輸出 1 2 3
1,2,3
```


## 其他問題

with open(file, newline='') 的newline=''到底在幹嘛...


