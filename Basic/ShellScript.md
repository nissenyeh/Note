# Shell Script

## 基本說明

- 變數要用`$`表示
- `$0`、`$1` 表示command line傳入的`參數`

## 迴圈

- {1..10}表示從1~10
- do ... done 的裡面會執行程式

```shell
for i in {1..10}
do 
 echo $i
done
// 1,2,3,4,5,6,7,8,9,19
```

迴圈如果會用到「變數」要改用`seq`

```shell
for i in $(seq 1 $1)
do
  touch $i.js;
  echo $i
done
// 輸入3，可以產生1.js,2.js,3.js檔案
```

## 爬蟲

- `curl`:可以用來獲取網站
- [pup](https://github.com/ericchiang/pup): pup is a command line tool for processing HTML

```shell
curl  https://github.com/$1 | \
      pup  'span.vcard-fullname,'\
            'div.js-user-profile-bio,'\
            'span.p-label,'\
            'a[rel="nofollow me"] text{}'
```

## 執行shell Script

- $ ./test.sh  或是 sh test.sh
- 第一種方法要用`chmod` +x test.sh更改權限(`ll`可以看到權限）
