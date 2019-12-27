# Dcard購物版的關鍵字分析 <br/> Dcard Online Shopping Board Keyword Analysis


## 專案介紹 Introduction

分析 2018-2019 Dcard（台灣最大的匿名交流平台）網路購物板數據。使用SQL和Python進行關鍵字分析，並藉此觀測大學生對各種購物平台的評價

Analyzed 'Dcard' (Taiwan's largest anonymous communication platform) online shopping board data for keyword analysis with SQL, Python and observe consumers' evaluation for various shopping platforms

## 專案結果 Analysis Results

## 1. Dcard「網路購物版」文章標題常見出現的購物平台？ <br/> What are the common shopping platforms that appear in the Dcard online shopping board?

### 次數分析 Frequency analysis


After segmenting words from article, we can find that Shopee (蝦皮購物) and Taobao (淘寶網) are the most common platforms consumer uses. Meaningful vocabulary statistics are roughly as follows:
- Shopee：1094 times
- Taobao：526 times


根據文章斷詞後，可以發現蝦皮、淘寶網是最常出現的平台。有意義的詞彙統計大致如下：
- 蝦皮 1094 次
- 淘寶 526  次
.
.
.
（下略）


The code is as follows：
```py
#目標：計算每個詞彙在所有文檔中出現的次數

# 1.引入套件
import jieba #jieba是斷詞套件
import csv
file_content = 'title.csv'  #dcard網路購物版的標題資料
file_stop = 'stop_words.txt'  #停止詞彙，可以設定這個檔案，讓太通俗不會計算進去

# 2.進行切詞
segments = []
with open(file_content, 'r') as csvfile:  
     segments += jieba.cut(csvfile.read())  #將切詞的結果會傳到陣列中

# 3.計算每個詞的出現次數        
dic = {}
for ele in segments:
    if ele not in dic:
        dic[ele] =1
    else:
        dic[ele] = dic[ele] +1
        
# 4.輸出結果
import operator 
sorted_word = sorted(dic.items(),key=operator.itemgetter(1),reverse=True)
for ele in sorted_word:
    print(ele[0],ele[1])
```

### 關鍵字分析 TF-IDF analysis

According to the `TF-IDF` algorithm, it is found that the important keywords are as follows. It can be seen that the most commonly used platforms for Dcard Online Shopping Board users are Shopee (蝦皮購物) and Taobao (淘寶網)

- Shopee 0.3572193720138916 （TF-IDF score）
- Taobao 0.17175264138876326（TF-IDF score）

根據`TF-IDF`演算法發現重要的關鍵字如下，可知Dcard「網路購物版」版友最常使用的平台依然是蝦皮和掏寶。

- 蝦皮 0.3572193720138916
- 淘寶 0.17175264138876326


```py
#計算文章的關鍵字 （利用的jieba的TF-IDF算法）
import jieba.analyse

with open(file_content, 'r') as csvfile:  
     s = csvfile.read()

print(jieba.analyse.extract_tags(s, topK=100, withWeight=False, allowPOS=()))
for x, w in jieba.analyse.extract_tags(s, withWeight=True):
     print('%s %s' % (x, w)) #分數結果愈大就是關鍵字。例如 蝦皮 0.3572193720138916 > 賣家 0.22530289459742706，表示蝦皮是關鍵字
```

## 2. What is the user's frequent comment for Shopee (蝦皮購物) and Taobao (淘寶網)

From the keyword heatmap, you can find:
- Users often complain about Shopee (蝦皮購物) sellers on the Dcard shopping board, because the most commonly mentioned keywords for Shopee (蝦皮購物) are "Hate", "Return", "Seller"
- Users have a better evaluation of Taobao (淘寶網) in the Dcard shopping board. The most commonly mentioned keyword is "Product consolidation"(集運)


從關鍵字熱圖(heatMap)可以發現：
- 用戶在Dcard購物版上最常抱怨蝦皮的賣家，因為蝦皮最常一起被提到的關鍵字是「黑特」、「退貨」、「賣家」
- 用戶在Dcard購物版上對淘寶網的評價較好，因為淘寶最常一起被提到的關鍵字是「集運」

![Alt text](img/dcard網路購物版.png)

The code is as follows：

```py
# 關鍵字共現矩陣1：關鍵字＆關鍵字的共現矩陣matrix   
# 例如：計算「蝦皮」跟「黑特」同時在文章中出現（共現）過幾次，次數愈多表示「蝦皮和黑特」容易一起出現

import jieba
import csv
file_content = 'makeup.csv'  #csv檔案路徑

# 1.把每一行資料拖出來並進行切詞
originlines=[]
with open(file_content, 'r') as csvfile:  
     lines = csv.reader(csvfile)
     for line in lines:
         segment = jieba.cut(line[0]) # 把每一行的詞切好後回傳該陣列
         line = []
         for i in segment:
            line.append(i)
         originlines.append(line)  
         
# 2.建立矩陣
print('generate the matrix')

highfrequencyword = ['粉底','顏色','推薦'] # 這邊輸入想要分析的關鍵字

wordcount=len(highfrequencyword)
cormatrix= [[0 for col in range(wordcount)] for row in range(wordcount)] #建立都是0的矩陣
for colindex in range(wordcount):
    for rowindex in range(wordcount):
        cornum=0
        for originline in originlines :
            if highfrequencyword[colindex]  == highfrequencyword[rowindex]:
                continue
            if highfrequencyword[colindex] in originline and highfrequencyword[rowindex] in originline:
                cornum+=1
        cormatrix[colindex][rowindex]=cornum

print(cormatrix)

# 3.寫入矩陣
print('write matrix to file matrix.csv!')
writer=csv.writer(open('matrix.csv', 'w'))  #輸出matrix的檔案
writer.writerow(highfrequencyword)
for item in cormatrix:
    writer.writerow(item)
print('matrix OK!')
```

```py
# 關鍵字共現矩陣2：關鍵字＆關鍵字的共現矩陣matrix，[['蝦皮', '蝦皮', 0], ['蝦皮', '賣家', 221],
# 例如：計算「蝦皮」跟「黑特」同時在文章中出現（共現）過幾次，次數愈多表示「關於蝦皮的黑特文」多

import jieba
import csv

file_title = 'title.csv'  #csv檔案路徑

# 1.把每一行資料拖出來並進行切詞
originlines = [] 
with open(file_title, 'r') as csvfile:  
     lines = csv.reader(csvfile)
     for line in lines:
         segment = jieba.cut(line[0])
         line = []
         for i in segment:
            line.append(i)
         originlines.append(line)  
         
# 2.建立矩陣
print('generate the matrix')

cormatrix = []
highfrequencyword = ['蝦皮','淘寶','黑特','賣家','問題','代購','推薦','請問','購物','請益','網購'] # 這邊輸入想要分析的關鍵字
wordcount=len(highfrequencyword)

for i in range(wordcount):
    for j in range(wordcount):
        cornum=0
        for originline in originlines:
            if highfrequencyword[i]  == highfrequencyword[j]:
                continue
            if highfrequencyword[i] in originline and highfrequencyword[j] in originline:
                cornum+=1
        cormatrix.append([highfrequencyword[i],highfrequencyword[j],cornum])
          
print(cormatrix)
    
# 2.寫入矩陣

print('write matrix to file newmatrix.csv!')
writer=csv.writer(open('newmatrix.csv', 'w'))
for item in cormatrix:
    writer.writerow(item)
print('matrix OK!')
```

```py
import numpy as np
import matplotlib
import matplotlib.pyplot as plt

print(matplotlib.matplotlib_fname()) #印出文字設定路徑


vegetables = ["蝦皮","掏寶"]  #Y軸資料

farmers = ["黑特","退貨","取貨","賣家","買家","集運","網購","推薦","代購","問題","請問","購物","請益","詢問","分享","買過","怎麼","有人"]
#X軸資料

font = {'family' : 'SimHei', #設定文字樣式
        'weight' : 'bold',
        'size'  : '20'}

matplotlib.rc('font', **font)

harvest = np.array([ #把matirx丟進去
[85,63,31,221,44,2,6,14,18,66,6,55,18,16,21,4,18,12],  #一列資料
[7,5,7,3,0,78,1,14,0,70,1,6,9,6,22,1,3,2]  #一列資料
])

fig, ax = plt.subplots(figsize=(20,20)) #設定圖片大小
im = ax.imshow(harvest)

# We want to show all ticks...
ax.set_xticks(np.arange(len(farmers)))
ax.set_yticks(np.arange(len(vegetables)))
ax.tick_params(top=True, bottom=False,  #把x軸放到上面
               labeltop=True, labelbottom=False)
# ... and label them with the respective list entries
ax.set_xticklabels(farmers)
ax.set_yticklabels(vegetables)

# Rotate the tick labels and set their alignment.
plt.setp(ax.get_xticklabels(), rotation=0, ha="right",
         rotation_mode="anchor")

# Loop over data dimensions and create text annotations.
for i in range(len(vegetables)):
    for j in range(len(farmers)):
        text = ax.text(j, i, harvest[i, j],
                       ha="center", va="center", color="w")


ax.set_title("關鍵字熱圖")  #設定標題
fig.tight_layout()
plt.show()
```