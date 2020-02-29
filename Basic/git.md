# Git


### 強迫把remote master拉下來

- 有時候想強迫把remote master拉下來，完全不合併

```shell
git fetch --all
git reset --hard origin/master #表示把遠端的master強迫拉下來
git reset --hard origin/<branch_name>  #表示把遠端的branch強迫拉下來
```

### 把git add undo 

- 後悔git add 

```
git reset <file> 
```
### git reset  

- 已經commit，想要回復之前的commit
- 已經pull，想要後悔

``` Shell
git reset --hard
```

### git checkout -- file 

- 還沒commit，想要捨棄所有的改變

```Shell 
git checkout -- . : drop all changes which is not committed yet
git checkout <file>. : drop all changes in specific file which is not committed yet
```

### change previos commit message 

- 後悔的想要改上一個commit的訊息了

```Shell
git commit --amend : change previos commit message 
```



### git stash

- 想要切換分支，但是又不想要把目前改動的程式提交commit

```Shell
git stash : temporarily save changed file
git stash list : list stash
git stash pop : take changed file back
git stash drop : drop changed file 
```