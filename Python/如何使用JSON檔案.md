
## 如何使用JSON檔案？



```py
import csv  #引入CSV
file = 'dic.csv'  #csv檔案路徑 

with open(file, newline='') as csvfile: # 打開成csvfile檔案
     data = list(csv.reader(csvfile))  #把檔案轉成一個陣列

for row in data:
    print(row)  #印出每行的資料
```