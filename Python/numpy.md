# NumPy

- NumPy是一個重要的第三方庫，提供數據分析所需要的數據結構
https://www.scipy.org/install.html

## 為什麼不用python內建的數據結構？

## 安裝Numpy

- 用pip安裝Numpy

```
python3 -m pip install --user numpy scipy matplotlib ipython jupyter pandas sympy nose
```

### Numpy的數列是多維的


- python內建的數列，只有一個維度
- Numpy提供的數列，可以有多個維度

``` py
import numpy as np
a =[[1,2,3],[4,5,6]]
b = np.array([[1, 2, 3], [4, 5, 6]])
print(a)
## [[1, 2, 3], [4, 5, 6]]
print(b)
##[[1 2 3]
##[4 5 6]]
```


- 多度數列的取值方式也不太一樣

``` py
import numpy as np
b = np.array([[1, 2, 3], [4, 5, 6]])
print(b[0]) # 獲取第0列的所有數據
## >> [1 2 3]
print(b[0,1]) # 獲取第0列，第1欄的數據
## >>  2
```

### Numpy的常用函式

- array([]) : 建構一個多維數組
- shape: 查看數組有多少列、欄
- dtype: 查看元素的數據屬性

```python
a = np.array([[1, 2, 3, 5], [4, 5, 6, 6],[4, 5, 6, 6]])
a.shape()  
## => (3,4)  有3列，有4欄
a.dtype()  
## => int64
```

#### 自定義數組結構

- 感覺跟物件有點像，但好像又不太一樣？

```py
a = np.array([[1, 2,
persontype = np.dtype({
  'names': ['sutdentName','Math','Chinese','English'],
  'formats':['S32','i','i','i']
})

studentScore = np.array([
  ('nissen',100,90,70),
  ('EK',90,80,100),
  ('Andrea',85,70,100)
],dtype = persontype)

print(studentScore['name']) # ['nissen','EK','Andrea']
print(np.mean(studentScore['Chinese'])) # 80.0
```

#### 建立等差

- np.arange(初值,終值,步長)
> np.arange(1,11,2) 建立從1~11，差距為2的等差數組
- np.linspace(初值,終值,元素個數)
> np.linspace(1,9,5): 建立從1~9，差距為5的等差數組

#### 統計函數

- 最小值 amin(list,axis)
- 最大值 amax(list,axis)


``` py
import numpy as np
a = np.array([[1,2,3], [4,5,6], [7,8,9]])
print np.amin(a)   # 對所有元素進行元素
# >> 1 
print np.amin(a,0)  # [1,2,3], [4,5,6], [7,8,9]進行比較
# >> [1,2,3] 
print np.amin(a,1) # 從每個陣列中選最小的元素
# >> [1,4,7] 

```

- 最大和最小值之差 ptp(list,axis)

``` py
import numpy as np
a = np.array([[1,2,3], [4,5,6], [7,8,9]])
print(np.ptp(a)) # 
# >> 8  >> 最大:9 最小:1
print(np.ptp(a,0))
# >> [6,6,6]  >> 最大:[7,8,9] 最小:[1,2,3]
print(np.ptp(a,1))
# >> [2,2,2]  >> 每個數組都計算最大,最小的差，[3-1],[6-4],[9-7]

```

- 百分位数 percentile()

```PY
import numpy as np

a = np.array([[1,2,3], [4,5,6], [7,8,9]])
print(np.percentile(a, 50))
# >> 5  >> 1,2,3,4,5,6,7,8,9 進行比較
print(np.percentile(a, 50, axis=0))
# >> [4,5,6]  >> [1,2,3], [4,5,6], [7,8,9] 進行比較
print(np.percentile(a, 50, axis=1))
# >> [2,5,8]  >> [1,2,3], [4,5,6], [7,8,9] 個別進行比較
```

中位数 median()、平均数 mean()

``` py
import numpy as np
a = np.array([[1,2,3], [4,5,6], [7,8,9]])
# 求中位数
print(np.median(a))
  # >> 5.0 >> 1,2,3,4,5,6,7,8,9 去求中位數
print(np.median(a, axis=0))
  # >> [4,5,6]  >> [1,2,3], [4,5,6], [7,8,9] 進行運算
print(np.median(a, axis=1))
  # >> [2,5,8] >> [1,2,3], [4,5,6], [7,8,9] 個別進行比較

# 求平均数
print(np.mean(a))
  # >> 5.0  >> 1,2,3,4,5,6,7,8,9 進行平均
print(np.mean(a, axis=0))
  # >> [4,5,6]  >> [1,2,3], [4,5,6], [7,8,9]  相加進行平均
print(np.mean(a, axis=1))
  # >> [2. 5. 8.]  >> [1,2,3], [4,5,6], [7,8,9] 個別相加進行平均
```

標準差 std()、方差 var()

- 方差的計算是指每個數值與平均值之差的平方求和的平均值
- 標準差是方差的算術平方根，代表的是一組數據離平均值的分散程度

```py
a = np.array([1,2,3,4])
print np.std(a)
print np.var(a)
```

排序 sort()

```py
a = np.array([[4,3,2],[2,4,1]])
print(np.sort(a))
print(np.sort(a, axis=None)) #從最裡面那軸看
print(np.sort(a, axis=0))
print(np.sort(a, axis=1)) #從最裡面那軸看 
# >>[[2 3 4]
#    [1 2 4]]
# >> [1 2 2 3 4 4]
# >>[[2 3 1]
#    [4 4 2]]
# >> [[2 3 4]
#    [1 2 4]]
```


####  Numpy不太好懂的地方

1. Numpy的Array跟內建的有什麼不ㄧ樣？

Numpy的Array是多維度的，但內建的list只有一維

2. axis是什麼？

- axis是數組的層級

``` python
[
  [1,2,3]
  [4,5,6]
]
```

可以想像[]是一道門，@w@代w表眼睛
當axis= 0 的時候，此時@@會在第一道門裡面看到兩個元素[1,2,3],[4,5,6]
``` python
[ @w@ # @@「哦！這裡有2個陣列耶」
  [1,2,3]
  [4,5,6]
]
```
> @@是假想的眼睛

當axis= １ 的時候，此時@@會在第二道門裡面看3個元素 

``` python
[ 
  [@w@ 1,2,3] # @@「哦！這裡有3個元素」
  [@w@ 4,5,6] # @@「哦！這裡有3個元素」
]
```

