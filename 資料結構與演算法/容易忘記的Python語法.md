
# 容易忘記的Python語法

## For
- `遍歷`：for i in "banana"
- `要數字的`：for i in `range(1, 6)`
- `要index的`：for (index,i) in enumerate(sm)
- `多對一字典`:myDict.update(dict.fromkeys([1,2,3], [3]))

## for 和 if 的合併

- (x for x in xyz if x not in a)或是[x for x in xyz if x not in a]

```py
# 找出不在xyz中的值
a = [2,3,4,5,6,7,8,9,0]
xyz = [0,12,4,6,242,7,9]
gen = (x for x in xyz if x not in a)

for x in gen:
    print(x)
```

# 做字典

```py
    d = {}
    for i in arr:
        if i in d: d[i] +=1
        else: d[i] =1
```

# 餘數

n//2：求除數
n%2：求餘數