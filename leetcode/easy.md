
# 心得總結

- 先用紙筆設計再實作是王道
- 到底是寫得多好，還是一題不停優化好呢？


# 紀錄

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


### 2. maximum-69-numbe

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

### 3. split-a-string-in-balanced-strings

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

### 4. to-lower-case

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

### 5.unique-number-of-occurrences

```py 
class Solution:
    def uniqueOccurrences(self, arr):
        dict1 ={}
        for i in arr:
            if i in dict1:dict1[i] += 1
            else: dict1[i] = 1
        print(dict1)

        dict2={}

        for ele in dict1:
            if dict1[ele] in dict2:return False
            else: dict2[dict1[ele]] =1

        return True
```

- 要更快怎麼那麼難QQ

Runtime: 48 ms, faster than 14.07% of Python3 online submissions for Unique Number of Occurrences.
Memory Usage: 12.9 MB, less than 100.00% of Python3 online submissions for Unique Number of Occurrences.


#### 6. sort-array-by-parity
```py
class Solution:
    def sortArrayByParity(self, A):
        even = []
        odd = [] 
        for i in A:
            if i % 2 == 0:
                even.append(i)
            else:
                odd.append(i)
        return even+odd
```

- 這題目特簡單耶（爽）
- Runtime: 184 ms, faster than 5.13% of Python3 online submissions for Sort Array By Parity. （靠腰，都這麼簡單還可以更快喔）
- Memory Usage: 13.1 MB, less than 100.00% of Python3 online submissions for Sort Array By Parity.


### 7.find-n-unique-integers-sum-up-to-zero

```py
class Solution:
    def sumZero(self, n):
        
        pair = n // 2
        arr = []
        count = n
        for i in range(pair):
            arr.append(count)
            arr.append(-count)
            count += 1

        print(arr)

        if(n%2==0):return arr
        else: arr.append(0)

        return arr
```

- 莫名其妙faster than 96.57% of Python3 ，覺得很荒謬
- Runtime: 24 ms, faster than 96.57% of Python3 online submissions for Find N Unique Integers Sum up to Zero.
- Memory Usage: 12.8 MB, less than 100.00% of Python3 online submissions for Find N Unique Integers Sum up to Zero.


### 8.decompress-run-length-encoded-list

- 頗簡單，有用筆打草稿基本就簡單
- Runtime: 68 ms, faster than 67.53% of Python3 online submissions for Decompress Run-Length Encoded List.
- Memory Usage: 13 MB, less than 100.00% of Python3 online submissions for Decompress Run-Length Encoded List.

```py
class Solution:
    arr = []

    def decompressRLElist(self, nums):
        self.arr=[]
        i = 0
        for x in range(len(nums)//2):
            self.puush(nums[i],nums[i+1])
            i+=2
        return self.arr
    
    def puush(self,times,num):
        for i in range(times):
            self.arr.append(num)
```


### 9.find-numbers-with-even-number-of-digits

```py
class Solution:
    def findNumbers(self, nums):
        count = 0
        for i in nums:
            digit = len(str(i))
            if digit % 2 == 0:
                count+=1
        return count
```

- 好像有點簡單
- Runtime: 52 ms, faster than 73.08% of Python3 online submissions for Find Numbers with Even Number of Digits.
- Memory Usage: 12.7 MB, less than 100.00% of Python3 online submissions for Find Numbers with Even Number of Digits.