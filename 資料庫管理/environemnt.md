# 資料庫架構


- DBMS：操作資料儲存的系統，比如說MySQL是DBMS，他可以去操作底層硬體的資料儲存方式，也可以連接到遠端的機器去操作資料儲存。

![RelationShip](./圖片/clientType.png)

- Fat Client：主要由Client負責運送，但會導致Client的工作量很重
    - Server：儲存資料
    - Client：去Server用SQL拿資料＋運算＋畫面呈現
> 每個Client都要裝DBMS（像是MySQL）去操作資料庫
> 缺點：
- Thin Client：主要由Server負責儲存資料＋資料存取＋運算
    - Server：儲存資料＋資料存取＋運算
    - Client：畫面呈現
> 像是ATM就屬於Thin Client架構，介面只有很簡單的功能，完全讓遠端伺服器操控。
> 缺點是Serve可能loading太重。
- Distributed：平均分配運算
    - Server：儲存資料＋資料存取＋部分資料運算
    - Client：畫面呈現＋部分資料運算


## One tier

## Two-Tier Database Server

- Client：讀取資料庫並且進行資料運算
- Database server:儲存資料

## Three-Tier Architectures:

- Client：呈現畫面
- Application server：處理商業邏輯
- Database server:儲存資料


## ODBC（Open Database Connectivity）

提供API，讓一般的應用程式可以用自己的程式語言去存取資料庫的內容。

- ODBC：提供API，讓一般的應用程式可以用自己的程式語言去存取資料庫的內容
- JDBC：
- ADO.NET：






