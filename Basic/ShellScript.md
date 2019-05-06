### Shell Script

#### 基本說明

- 變數要用`$`表示
- `$0`、`$1` 表示command line傳入的`參數`

#### 迴圈

- {1..10}表示從1~10
- do done裡面執行迴圈程式

```
for i in {1..10}
do 
 echo $i
done
```

迴圈如果會用到變數要改用`seq`

```
for i in $(seq 1 $1)
do
  touch $i.js;
  echo $i
done
// 輸入3，可以產生1.js,2.js,3.js檔案
```

#### 執行shell Script

- $ ./test.sh  或是 sh test.sh
- 第一種方法要用`chmod` +x test.sh更改權限