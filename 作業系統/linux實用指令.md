


# shell 指令

## 實用指令


```shell
sudo -s #切換到superuser do，之後sudo指令就不用再輸入密碼
exit #離開

```


檔案檢視與資料夾操作
```shell
~ # 代表了家目錄，可以不用 cd ../../code 可以直接  ~/code
ls -a # 可以看帶點的檔案
ls -l # use a long listing format以長格式表示，包含檔案屬性。
pwd # print working directory]
cd # change directory 
cp # copy  來源 到 目的地  例如：cp ./hi.txt  ~/
cp -r # copy 把整個資料夾複製起來
mv # move  來源 到 目的地  例如：mv ./hi.txt  ~/ 
   # move 也可以重新命名  例如：mv ./hi.txt  ./bye.txt
cat # 把檔案內的資料列出來 例如 cat note.txt
rm # 刪掉資料，垃圾桶只是一個假個資料夾
rm -r # 刪掉只個資料夾
rmdir -r # 把整個資料夾刪掉
mkdir # make directory
mkdir -p a/b/c # 一次建立一連串的路徑
find ./ -name 'hi' # 從 ./開使找名為hi的檔案
grep -r 'text' file   # 從 file 檔案中找到'text'文字
grep -rl 'text' file # 只回覆有'text'文字的檔名，而不要把所有文字列出來
wget http://goo.gl/12345 # 發送get指令
```

管線命令（輸出資料，丟給下一個指令用）
```shell
ls | wc -l #秀出ls的資料，但丟到wc去看有幾行
tail -f 'server.log' | grep 'error' -C  #去看末尾的資料，但是只顯示有error的部分
cat fileName | sort | unique | wc -l #去把檔案內容排序、找出唯一值、去看有幾行（這個在看server ip是很方便，可以看到有多少不重複的IP）
```



暱稱
```shell
alias qq= 'ls -l'
```

檢視檔案內容
```shell
gedit abc # 編輯檔案
less file # 檢視檔案
cat file # 列出檔案中的文字
head fileName -n 3 # 從前面看前3筆資料
tail fileName -n 9 # 看後面看後9筆資料
tail -f server.log # 去即時的去看server.log的末端檔案
grep 'error' fileName - C 4 #從「fileName」找到error，還有列出上下各4行
wc -w # watch word 看檔案中有幾個字
wc -l # watch line 看檔案中有幾行
```


檔案更新
```shell
sudo apt-get update # 更新
sudo apt-get install sl # 安裝「sl」套件
sudo apt-get remove sl # 刪除「sl」套件
```

砍掉佔用port的程序
```
sudo lsof -i :3000
kill -9 {PID}
```

資訊顯示
```shell
man ls # manual 查詢可使用參數
whoami # 查詢使用者是誰？
uname -a # 看到kernel的狀態
ifcongfig # 看網卡資訊
top # 列出系統上最吃CPU 與記憶體的程式。
history # 看過去有過的指令 用驚嘆號執行，!20
（或是用control + R 搜索）
```

在top中，其中load average（平均附載）:0.00（最近 1 分鐘） , 0.01（最近 5 分鐘） , 0.05（最近 15 分鐘）
Load Average 的數字代表有多少個 process 在等待 CPU 及 DISK I／O 等資源運算，如果是 1 表示有一個 process 正在執行或等待 CPU 運算；5 表示有 5 個 process 正在執行或等待 CPU 運算，一台完全閒置的電腦，其 Load Average 是 0.


開關機
```shell
shutdown # 關機（把遠端機器shutdown就gg了）
reboot # 重開機 
```

帳號管理
```shell
sudo adduser 使用者名稱 # 新增使用者
su 使用者名稱 # 用使用者名稱登入（但要exit才真的原帳號退出）
deluser 使用者名稱 # 刪除使用者
```

> 使用者會在 ./home 目錄下


網路相關
```shell
ping 8.8.8.8 # 連到ip
host google.com #去找DNS做名稱解析
```



殼程式

```shell
echo $0 # 可以知道shell程式的類型
chsh # change shell 更換殼成式
```

## IO重導向

- 把output導向到別的地方上

```shell
echo 'hello' > file  # 把echo 'hello'的輸出資料「複寫」到file
echo 'hello' >> file  # 把echo 'hello'的輸出資料「接續」載入到file  
find / -name 'file' 1>suc.log 2>/err.log # 把錯誤代碼的資料丟到err.log
find / -name 'file' 1>suc.log 2>/dev/null #把錯誤代碼的資料丟到file  
```

## 環境變數

### 目錄


-  `/` 根目錄
-  `./` 是當前目錄
-  `~/` 是家目錄



### 公有設定檔

/etc/bashrc

### 私有設定檔

~/.bashrc

## for 迴圈

```shell
for i in {1..60}; 
do echo '健康飲食Day'$i ;
done
```

## 視窗指令

```
control+l  # 把shell指令清掉
command+shift+t #重開關掉視窗 (for瀏覽器)
```

## 如何自訂腳本？


1. 如果是使用zshrc作為shell的環境，就可以去 ~ 目錄下，找到 `~/.zshrc`，並且設定alias

```shell
alias gitnote="git add . && git commit -m 'update' && git push -u origin master"
```

2. 完成後重新開啟終端機，下次他就會自動source 該 script，並設定alias。



# 練習題目

```
3
1
4
4
2
3
5
6
7
3
4
5
6
```

- 請找出有幾個不重複的數字？