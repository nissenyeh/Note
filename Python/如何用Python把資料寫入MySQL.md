# 如何用Python把資料寫入MySQL

## 安裝mysql.connector

```
pip3 install mysql-connector-python
```

## 寫入資料庫

```py
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="root",
  passwd="password",
  database="dcard" #schema的名稱
)

mycursor = mydb.cursor()

sql = "INSERT IGNORE INTO more (id, title, comment_count,like_count, createdAt, school, content VALUES (%s, %s, %s, %s, %s, %s, %s)"
val = (article_id, title ,commentCount, likeCount, createdAt, school, content)
mycursor.execute(sql, val)

mydb.commit()

print(mycursor.rowcount, "record inserted.")
```