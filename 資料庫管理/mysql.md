# Mysql的基本操作


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
