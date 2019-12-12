# 如何將CSV建立成「多對一」字典?


目標：將csv檔案轉變成`多對一`的字典，比如說當輸入「阿尼森」、「尼森」、「nishan@nissenlab.org」時，一率輸出nishan

```
阿尼森,尼森,nishan@nissenlab.org,nishan
```


## 步驟

1. 準備`.csv`檔案，格式如下

```csv
阿尼森,尼森,nishan@nissenlab.org,nishan
劉惠恩,惠恩,hauant@nissenlab.org,hauant
張家文,家文,chawun@nissenlab.org,chawun
陳雨凡,雨凡,wufani@nissenlab.org,wufani
劉敏橋,敏橋,minchia@nissenlab.org,minchia
張立婷,立婷,liting@nissenlab.org,liting
彭立凡,立凡,lifang@nissenlab.org,lifang
李恩婷,恩婷,anting@nissenlab.org,anting
```
> 以此CSV檔案為例，最後一欄位放置「預期輸出的結果」


2. 建立python腳本，程式碼如下

```py
import csv
file = 'dic.csv'  #csv檔案路徑 

with open(file, newline='') as csvfile:
    data = list(csv.reader(csvfile))  

myDict = {}

for row in data:
    myDict.update(**dict.fromkeys(row, row[3])) #最後一個值，應該放置預期輸出的欄位，不一定是3


print(myDict['尼森']) #一律會輸出nishan
print(myDict['阿尼森']) #一律會輸出nishan
```

3. 執行python腳本

```
python3 script.py
```

## 詳細說明

### 1.先將csv資料輸出成一個「存放多陣列」的陣列
```py
import csv
file = 'dic.csv'  

with open(file, newline='') as csvfile:
    data = list(csv.reader(csvfile))  

# 會輸出：
# [[阿尼森,尼森,nishan@nissenlab.org,nishan],
# [劉惠恩,惠恩,hauant@nissenlab.org,hauant],
# [張家文,家文,chawun@nissenlab.org,chawun],
# [陳雨凡,雨凡,wufani@nissenlab.org,wufani],
# [劉敏橋,敏橋,minchia@nissenlab.org,minchia],
# [張立婷,立婷,liting@nissenlab.org,liting],
# [彭立凡,立凡,lifang@nissenlab.org,lifang],
# [李恩婷,恩婷,anting@nissenlab.org,anting]]  

```

- `csv.reader()` 會在讀取csv檔案後，回傳一個物件
- `list()` 則把該物件轉成一個[[a1,a2,a3,a4],[b1,b2,b3,b4]...]的陣列檔案

### 2.把「多陣列元素」轉換成字典

```py
myDict = {}

for row in data:
    myDict.update(**dict.fromkeys(row, row[3]))
```

- `dict.fromkeys([儲存key陣列],value)`：會把陣列中的所有值當作key，並為一輸出value。例如

```py
dic =  dict.fromkeys([1,2,3],3)
prit(dic[1]) #會得到3
```

- myDict.update(`**`dict.fromkeys(row, row[3])):會把所有的key,value拿出來，並且更新到myDict中

