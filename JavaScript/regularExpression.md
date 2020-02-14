
# Regular Expression


| 匹配  |  回傳 |  範例 |  
|---|---|---|
| \d | 數字  | 1234 => 匹配 1,2,3,4 單一數字|
| \D  | 非數字  | sb1234 => 匹配 s,b 單一字符||
| \w  | 文字 (a-z,A-Z,0-9,_)  | sb1234 => 匹配 s,b,1,2,3,4 單一字符||
| \W  | 非文字  |@12a,c=> 匹配 @ , 單一字符||
| \s  | WhitSpace | 1 3 匹配「 」單一空白字符|
| \S |  Non-WhitSpace |1 3 匹配1,3等單一空白字符 |
| \b |  Word-Boundary | \ba 會匹配「開頭為a」的字符，\b會回傳所有的boundary|
| \B |  non-WordBoundary |\Ba 會匹配「開頭不為a」的字符 |
| . |  所有字符 |會回傳所有字符|
| `\.` | 只有dot符號  |會回傳dot符號 |
| `^` | 開頭  | ^a會回傳「開頭為a」的字符 |
| `$` | 開頭  | b$會回傳「結尾為b」的字符 |
| `[1-9]` | 範圍  | `[1-9]`會匹配所有符合「1-9」的字符 |
| `\d{n}` | 範圍  | `\d{n}`只會匹配「n個」數字，多的就不管|
| `\d{n,m}` | 範圍  | `\d{n,m}`會回傳只少「n個一組」不然就是「m個一組」的數字 |
| `?` | 匹配0到1個字符   | 3? 如果字串有3匹配0~1次，就會匹配 |
| `+` | 匹配0到n個字符   | 3? 如果字串有3匹配0~n次，就會匹配 |
| `*` | 範圍  | 回傳0到多個字符 |

## 使用方式

```js
reg = /^[A-Z]{1}[1-2]{1}[0-9]{8}$/
reg.test(變數) // true or flase
```

## 常用

- [我討厭Regex!（實用網站）](https://ihateregex.io/)

- 身分證：`/^[A-Z]{1}[1-2]{1}[0-9]{8}$/`
- 居留證：`/^[A-Z]{2}\d{8}/`

## 例子

```
13.12 如果用 \d\d\.\d會匹配
13.1 如果用 \d\d.\d也會匹配
121212 如果用 \d{2} 會匹配到 12 12 12
first Last 和 first.Last 都會匹配 first.?Last
first Last 和 first.Last  和 first..Last  和 first...Last都會匹配 first.+Last
```


# 實用技能 Ternary if operator


 `判斷 ? a : b`
- 如果判斷為true，就執行a程式，否則執行b程式 



```js
const book = 1 
const answer = (book==1) ? '1本': '不只1本'  // 1 本

```

```js 
let book //  undefined
const answer = book ? '有書': '沒有書'  // 沒有書
```
##  ||  是什麼？


`const c = a ? a : b`
等價於
`const c = a || b`


var x = a || b || c 等价于：

```
var x;
if(a){
    x = a;
} else if(b){
    x = b;
} else {
    x = c;
}
```