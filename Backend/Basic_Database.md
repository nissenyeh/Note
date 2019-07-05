# Basic

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