# Mysql的基本操作


## 實用指令

### 「表格 table」的增刪改查

- 新增：CREATE TABLE tablename...
- 刪除：DROP TABLE tablename...
- 修改：ALTER TABLE tablename...
- 查詢：SHOW TABLE tablename...

```sql
CREATE TABLE talbe_name (欄位1 格式, 欄位2 格式)
```

### 「資料 data」的增刪改查

- 新增: INSER INTO tablename ... VALUES ...
- 刪除: DELETE FROM tablename ... where ....
- 修改: UPDATE tablename SET ... where ...
- 查詢: SELECT * or 欄位 from tablename where

###  表格table的「合併查詢」

#### 1. 使用 from 直接合併，然後用 where 篩選

```sql
SELECT * 
FROM 成員, 交友狀況
WHERE 成員居住地點= '台北' AND 成員.id = 交友狀況.id`
```

但這種做法不適用其中一邊的表格有「空直」得狀況

#### 2.使用 Left join 合併，然後用 on 去設定規則

```sql
SELECT  ...
FROM ...
Left join ... #join方式
on ... #join方式
```

```sql
// 查詢學期2019年有什麼課程，並且唯一查詢
select distinct(COURSE.CourseName)
from COURSE 
left join SEMESTER
on COURSE.CourseID = SEMESTER.SemesterID
where SEMESTER.year =2019
```

###  表格table的「合併計算」Group by

```sql
SELECT id , count(*) 
FROM 成員, 交友狀況
GROUP BY 成員.id
HAVING count(*)>=3
ORDER BY count(*) DESC;
```


- 遇到「合併計算」的時候就想到 GROUP BY，然後分別 select 名稱欄位、可以合併計算的欄位名稱
- 遇到「合併計算又要篩選」的時候，就想到 HAVING
- 遇到「排序」的時候就想到 ORDER BY

1. INSERT INTO ... VALUES  資料插入

```sql
INSERT INTO table_name
(column1, column2 , column3)
VALUES
(data1, data2, data3) // 如果不照順序，就可以指定欄位來排

or 

INSERT INTO table_name
VALUES (.....)  // 如果沒指定欄位，就會照順序排
```

例子

```sql
INSERT INTO CUSTOMER
VALUES (001,JACKSON,MALE)

INSERT INTO CUSTOMER
(INDEX, NAME, GENDER)
VALUES
(001,JACKSON,MALE)

INSERT INTO CUSTOMER
SELECT * FROM OTHERCUSTOMER
WHERE NAME = 'JACK'
```


2. DELETE FROM .... WHERE 刪除資料

```sql
DELETE FROM table_name 
WHERE  COLUMN = ''  #一定要指定條件

DELETE FROM table_name #這個指令會把所有row都刪掉，只剩下表格，要小心使用！！
```

```sql
DELETE FROM CUSTOMER
WHERE  NAME = 'JACKSON'
```

3. UPDATE .... SET  修改資料

```sql
UPDARE table_name
SET col = ''
WHERE col = ''

```
```sql
UPDARE customer
SET age = 12
WHERE name = 'jackson'
```

4. SELECT ... FROM 查詢資料

```sql
SELECT * 
FROM tablename
WHERE ...  
```

```sql
SELECT description, price
FROM product 
WHERE price > 300
```


## 運算子是有優先順序的

在where 中，可以使用運算子，但是要小心他們有順序，因此如果需要的話務必加上括號。

NOT > AND > OR 

```
DELETE FROM CUSTOMER
WHERE NAME = 'JACKSON' & AGE > 30 or AGE <20  
會被翻譯成名字叫JACKSON，年齡大於30歲的客戶，或是年齡大於20的客戶

WHERE NAME = 'JACKSON' & (AGE > 30 or AGE <20)
這樣才是名字叫JACKSON且年齡大於30或是小餘20歲的客戶

```

## 別名得使用

`as`：可以設定別名

```
SELECT p.name p.price
FROM product as p 
WHERE p.price > 300
```

## Like的使用

Like可以去進行模糊比對

- % ：匹配0~n個可能性 Mic* matches Mickey, Michael, Michelle, etc.
- ? ：匹配有一個字元 s?n matches sun, son, san, sin, etc.

```sql
select * from table
where name like '%lism'
order by id
```

## 函數的使用

- COUNT(), MAX(), MIN(), SUM(), AVG()…等


```sql
select COUNT(*) from table
where year like '%2015' // 找出 2015 年的資料有幾筆
```
- YEAR(), MONTH()

```sql
select * from Registration
where year(registrationDate) > 2008  // 搜尋2008年後的資料
```

- DISTINCT() 顯示不重複的資料

## order by 

- ASC：升冪排列
- DESC：降冪排列

```sql
根據名字筆畫升冪排列
select * from STUDENT
order by name ASC 
```

### 小練習

- 如何在student的表格中加上CLASS

alter table db.student 
add column Class VARCHAR()


### Relational algebra 關聯式

為什麼join和where的寫法都可以？

selecyt 垂直篩選
where 水平篩選

Cartesian Product 乘積運算：直接把兩個表格承在一起
Join 乘開後再用根據條件來去過濾

join很多次都還是表格，因為Relational algebra 有封閉性。


## datatype 

- INT：整數（可以存負數）
- VARCHAR：可以存文字，不管中英文。1個字，就是1個VARCHAR（雖然實際上英文用1個byte，中文用2個byte存）
- BLOB：可以上傳檔案
- DECIMAL：小數，DECIMAL(3,1)表示共有三位數，到小數點後一位，如23.1
- DATATIME：時間

## 設定

- PK：primary key 主鍵
- NN: Not Null 不能為空
- UQ：Unique index 不能重复（比如說name已經有一個Nissen，你就不能再加一個Nissen）
- ZF：是zero fill up 填充 0 的意思，比如var(3) 填1，就會變成001
- AI：是auto incrementail 自動增加，通常只有int才能用。隨著列的變多它會自動 0->1->2
- UN：是 Unsigned data type 沒有符號的資料，比如說你存-3，他就會幫你變成3
- BIN Is binary column 存放二進制數列