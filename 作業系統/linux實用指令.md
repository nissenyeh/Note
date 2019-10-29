

# shell 指令

## 實用指令

```shell
sudo -s #切換到superuser do，之後sudo指令就不用再輸入密碼
exit #離開
ls -a # 可以看帶點的檔案
ls -l # use a long listing format以長格式表示，包含檔案屬性。
sudo apt-get update # 更新
sudo apt-get update sl # 更新「sl」套件
sudo apt-get remove sl # 刪除「sl」套件
ping 8.8.8.8 # 連到ip
host google.com #去找DNS做名稱解析
```

#### for 迴圈

```shell
for i in {1..60}; 
do echo '健康飲食Day'$i ;
done
```

#### 視窗指令

```
control+l  # 把shell指令清掉
command+shift+t #重開關掉視窗 (for瀏覽器)
```

## 如何自訂腳本？


1. 如果是使用zshrc作為shell的環境，就可以去 ~ 目錄下，找到 `~/.zshrc`，並且設定alias

```shell
alias gitlazy="git add . && git commit -m 'update' && git push -u origin master"
```

2. 完成後重新開啟終端機，下次他就會自動source 該 script，並設定alias。

