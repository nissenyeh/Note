# Computer

## 計算機架構

一定包含Input、Output、CPU & memory、storage

- Input
- Output
- CPU & memory:
  - 暫時存在memory
  - 宣告變數的時候放到memory
  - 每個memory有address
- storage:永久儲存

```
num1 = 13 

// 在memory中的一個位置儲存放num1，然後賦值為13
num2 = 4 

// 在memory中的一個位置儲存放num2，然後賦值為4 
print(num1+num2) 

// 在memory中的一個位置儲存放num2，然後賦值為4 
// 當print出後，該memory的位置就會被清掉
```

Address         | Identifier  | Value | 
--------------|:-----:|-----:| 
0x20c630   | num1 |  13|   
0x22fd4c    | num2 |  4 | 
  |  |  |  
0x20c620   | (no name) | 17 |  

## 變數宣告

宣告變數