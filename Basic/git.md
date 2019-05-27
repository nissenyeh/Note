# Git

### git reset  

- 已經commit，想要回復之前的commit

``` t
`git reset HEAD^ -- hard` : go back to previous commit and drop all change
`git reset HEAD^ -- soft` : go back to previous commit and keep all change
```

### git checkout -- file 

- 還沒commit，想要捨棄所有的改變

```t
`git checkout -- .` : drop all changes which is not committed yet
`git checkout <file>. ` : drop all changes in specific file which is not committed yet
```

### change previos commit message 

- 後悔的想要改上一個commit的訊息了

```t
`git commit --amend`: change previos commit message 
```