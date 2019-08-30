
### Regular Expression

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