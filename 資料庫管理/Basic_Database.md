
### 資料庫



### 資料 

#### 資料 Data

- 結構型(Structured)：數字、文字、日期。例如：書名、作者...。
- 非結構型(Unsructured)：圖片、影片。例如：一段故事

#### 次資料 MetaData

MetaData：用來描述資料的data稱為MetaData
例如一本書的書名、字數、作者...就是MetaData。

### 訊息 Information

Data（資料）放在context（脈絡）中才會是訊息

### Schema

所謂的Schema是一種設計圖，定義了資料型別、描述、長度...等資訊。

### 為什麼需要資料庫?

- 資料庫：把資料有邏輯和系統整理的方式

1. 程式和資料不相依：一般的紀錄方式中，資料是放在程式中，它與程式有前後、規格上不統一個狀況
2. 不會有資料複製的問題：用一般的紀錄方式，容易會有資料複製後，大家版本都變得不一樣的問題。（例如：一個通訊錄發給10個人，A改了自己手機、B改了自己的地址，...結果最後就沒有一個最新和完整的版本）

#### 資料複製造成的問題

- 資料冗余(Data Redandancy)：浪費儲存空間
- 資料不一致(Inconsistence)：大家的儲存的版本都不一樣

#### ER-model

## 後端是什麼？

- 伺服器：處理Request、Response，例如:Apache、Node.js
- 資料庫：儲存資料（非必要），例如：MySQL、NoSQL

## 資料庫

- NoSQL(非關聯式資料庫) :
  -  Not only SQL，儲存任何資料型態，key-value
  -  不支援JOIN
  -  有點像是把JSON存進去資料庫


## Transaction 交易

每一次更改就是一次Transaction（可以一次更改多筆資料）

- A(atimicity)：一個Transaction中的更改要麼全部失敗、要麼全部成功
- C(consistency)：維持資料一制性
- I(isolation)：多筆資料不互相影響（不能同時更改一個職）
- D(Durabiluty)：交易成功後，資料不會不見

## Lock

- 當多個request同時到達的時候，可能會導致一筆資料同時被存取，造成Race condition的問題
- 可以在DataBase加上lock，把某個欄位鎖起來，避免被同時存取。