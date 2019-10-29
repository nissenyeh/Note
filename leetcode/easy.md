
### 1. Two Sum



```PY   
class Solution:
    def twoSum(self, arr, target):
        l = len(arr)
        for x in range(l):
            try:
              arr.index(target-arr[x])
              b = arr.index(target-arr[x])
              if(b!=x):
                return [x,b]                
            except ValueError:
              pass     
```

2019 10/27

- 很少用python寫程式，真的是很卡。原來for迴圈要用range()，原來查index要用index()，用來index會錯誤，所以要用try,except,pass
- 複雜度應該是O^2吧？（因為index是big(o),for也是big(o))
