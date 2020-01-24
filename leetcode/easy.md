
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


2. maximum-69-numbe

```py
def change(num: int)-> int:
    sm = str(num)
    arr = []
    for (index,i) in enumerate(sm):
        arr.append(i)

    recode = -1
    for (index,i) in enumerate(arr):
        if(i=='6'):
            recode = index
            break
        else:
            continue
    arr[recode] = "9"
    
    print(int("".join(arr)))


change("123")   
```

3. split-a-string-in-balanced-strings

```py
  def balancedStringSplit(self, s: str) -> int:
      arr = []
      for i in s:
          if(i=='L'):
              arr.append(-1)
          else:
              arr.append(1)

      print(arr)
      count = 0
      c = 0
      for i in arr:
          print('arr[i]',i)
          c = c+i
          print('c',c) 
          if(c==0):
              count=count+1
      return count
```

- 這題蠻有意思的，轉換一下視角算
- 但使用兩個for迴圈所以好像還是有點太耗資源嗎（？）

4. to-lower-case

```py
class Solution:
    arr = [
        ['A','a'],
        ['B','b'],
        ['B','b'],
        ['C','c'],
        ['D','d'],
        ['E','e'],
        ['F','f'],
        ['G','g'],
        ['H','h'],
        ['I','i'],
        ['J','j'],
        ['K','k'],
        ['L','l'],
        ['M','m'],
        ['O','o'],
        ['P','p'],
        ['Q','q'],
        ['R','r'],
        ['S','s'],
        ['T','t'],
        ['U','u'],
        ['V','v'],
        ['W','w'],
        ['X','x'],
        ['Y','y'],
        ['Z','z'],
    ]
    myDict = {}

    for (index,row) in enumerate(arr):
        myDict.update(dict.fromkeys(arr[index], arr[index][1]))

    def toLowerCase(self, s: str) -> str:
        arr=[]
        for i in s:
            if i in self.myDict:
                arr.append(self.myDict[i])
            else:
                arr.append(i)
        c="".join(arr)
        return c
```

- 這題覺得很難，真的真的可以直接硬幹一個字典嗎？這樣不犯法嗎？
- Runtime: 32 ms, faster than 11.35% of Python3 online submissions for To Lower Case.
- Memory Usage: 12.6 MB, less than 100.00% of Python3 online submissions for To Lower Case.