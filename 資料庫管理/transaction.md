
# Routines 自製SQL ＆Trigger 觸發SQL

## Routines 一段寫好的SQL語法

1. Function：會return
2. Procudure：單純執行程式，不return

```sql
CREATE OR REPLACE PROCEDURE productlinesale
    AS BEGIN
        UPDATE Product_T
            SET SalePrice = 90* ProductStandardPrice
            WHERE ProductStandardPrice >=400
    END;

EXEC productlinesale #執行指令
```

## Trigger 觸發

- 資料庫可以設定「一但ＸＸ」，就觸發ＯＯ行為。


可以設定一個TRIGGER，只要有人嘗試捨棄表格，就返回。
```sql
CREATE TRIGGER safety
ON DATABASE
FOR DROP_TABLE, ALTER_TABLE
AS 
    PRINT 'You must disable to drop or alter table!'
    ROLLBACK
```

# Transaction 交易


- 當我們在使用一些操作時（特別是交易）的時候，我們會希望保證每一次SQL都被完整執行，而不會產生執行到一半，然後斷電，資料就亂掉的狀況。因此可以使用`transaction`語法，去保證完整執行。（要麼完整執行、要麼都不會執行）

```sql
Begin transaction  # 開始交易
    UPDATE account SET amount=amount-100
    WHERE id=‘001’ and bank=‘A’

    UPDATE account SET amount=amount+100
    WHERE id=‘001’ and Timeline bank=‘B’
End transaction # 結束交易

```

- `COMMIT`：確認寫入資料庫
- `ROLLBACK`：恢復原本的樣子

資料庫在執行transaction之前，會先拍下一個快照(snapshot)。當SQL語法執行的過程中，如果發生了問題，就會恢復快照（rollback），否則就會確認改變（commit）


### ACID特性

關聯性資料庫，可以保證每個transactions（交易）都有以下特性

- A（Aitomicity）：不可分割性，比如說「A帳號-100，B帳號+100」，這樣的任務是不可被分割的，要麼就「完整執行」、要麼就「什麼是都不發生」。不會產生A帳號-100，然後斷電，B帳號沒有錢進來）的狀況。
- C（Consistency)：如果數據有一些限制，那從交易前到交易後都不會改變
- I（Isolatrion）：資料庫的結果不會呈現給使用者，直到transaction真的完成。比如以「A帳號-100，B帳號+100」的例子，不會發生使用者查詢餘額時看到A帳號-100，B帳號卻沒有錢的狀況。直到完整執行，才可能讓使用者看到最終結果。
- D（Durability）：只要transactions被commit，不管發生什麼錯誤、斷電，資料就會永遠改變，不會又跟你說「阿我資料沒寫進去」。


#### 


- UDT
- WINDOW