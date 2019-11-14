# MySQL效能

## 不要這樣寫SQL?

不要寫correlated subquery，這樣會複雜度會太高。

```sql
select ProductDescription, Producrfinish, ProductStandardPrice FROM Product_T 
    WHERE PA.ProductStandardPrice > ALL (SELECT ProductStandardPrice FROM Product_T PB WHERE PB.ProductID != PA.ProductID) # 在子查詢中PA.ProductID每次都不一樣，很浪費資源
```

改成non-correlated的版本

```sql
SELECT ProductDescription, ProductFinish, ProductStandardPrice
FROM Product_T PA
WHERE PA.ProductStandardPrice >= ALL (SELECT ProductStandardPrice FROM Product_T)
```

```sql
SELECT ProductDescription, ProductFinish, ProductStandardPrice
FROM Product_T PA
WHERE PA.ProductStandardPrice >= ALL (SELECT ProductStandardPrice FROM Product_T)
```

> 在子查詢中，最好一次就查完。

## 實用技巧

`EXPLAIN`：可以看每一個查詢花多久時間

```sql
EXPLAIN select * from table 
```