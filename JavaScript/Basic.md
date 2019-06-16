# Basic 


JS不是call by reference，也不是call by value，而是call by sharing。

```JavaScript
var arr = [1, 2, 3]
var newArr = arr
newArr[0] = 0
console.log(arr)  // [0, 2, 3]
```

## 物件(與屬性)、變數、型別的關係

### 物件（Object）是什麼？

- 定義：物件是記憶體中的資料，並藉由參考（變數）的方式進行拜訪。（因此用記憶體參考的資料，都可被稱為物件）
- 因為JS是物件導向的程式，因此所有的JS資料都是Object（包含undefined , 1 , '你好' 都是物件！）
- 但Object也可以分類為各種`資料型態`
  - 原生型態(Primitive type)：Number,undefined, null , boolean, string, symbol
  - 物件型態(Object type)

#### 屬性(Property)是什麼？

- 物件裡面`只有屬性`，沒有除了屬性之外的其他東西。
- 在全域環境中，window屬性就等於變數。

```js
var a = {
  name:"Neo",
  age:12
}
// a 下面有兩個屬性 name , age
// 而 name 和 age 會自己指向其他記憶體位置中的"Neo"和12
```




### 變數(Variable)是什麼？

- 變數：變數儲存了一個記憶體的位置（類似於指標），它會指向到一個物件

```js
var a = 1
```
電腦的步驟如下
1. 建立了一個1的物件 // 程式碼先從右邊開始執行
2. 建立了一個a的變數
3. 把儲存1物件的記憶體位置放到a裡面

> a 不等於 1 ， a只是指向了1的位置

### 型別(Type)是什麼？

JS是一個「物件導向」的程式語言，因此「全部都是物件」，只是不同物件會有不同的`型別`特徵。

> 型別只會在執行時才有，因為執行時才會有物件（記憶體）的問題

- 原始型別（Primitive Data Types) 
  - number
  - string
  - boolean
  - null
  - undefined
  - symbol
>＊無法擴增屬性，「不允許」擁有自己的屬性，但原始屬性有從父物件繼承來的屬性
- 物件型別(Object type) 
  - 原生物件
  - 宿主物件
>＊可以透過對父元件的擴充屬性，讓原始型別（Primitive Data Types) 可以使用一些原本沒有的功能。

```js
var a = 1
typeof(a) // number
a.name = "will"
console.log(a.name)  // undefined
```
-> 因為物件1是屬於原始型別，因此他不允許有屬性

```js
var a = 1 
Number.prototype.name = 2
a.name = 3
console.log(a.name) // 2
```

-> 因為物件1是屬於原始型別，因此他不允許有屬性




### 變數和屬性

```js
var a = 1;
window['a'] = 2;
delete window.a;
console.log(a); //  2  
//因為變數a等於window.a
```

```
b = 2;
delete b;
console.log(b); // Reference Error 
```

## 根物件與函式物件


### 根物件


執行環境本身會提供跟物件
- 瀏覽器: window
- NodeJS: global
- VueJS: vm.$root

以瀏覽器來說，會有一堆東西綁在window下，例如alert(),console()。物件只要有人可以參考到他，就不會被回收，所以會用物件只要被window連接就不會被回收。

如果物件鍊很長，那可以把屬性綁在根物件上就好！
```js
$('h2').hide('slow')
$('h2').show('slow') // 效率差，因為每次都建立一個$('h2')然後又回收掉
var h = $('h2') // 這樣就不會被回收掉了 
```



### 函式物件 Function

- 函式本身就是一種物件，並且可以被賦予屬性

```js
var a = function(){
  return 2
} 
a.x = 4 //這是合法的
```

- 函式的名字本身也是一種屬性
```js
var add = function add2(){ // 具名函示，給函式一個名字
  return 1
}
window.add.name // add2
--------------------

function add2() { 
  return 1
}
window.add2.name // 也是 add2
```
1. 建造一個function物件
2. 該物件有個name屬性叫做add2（名字其實沒啥意義）
3. 該物件的地址被存到add中

## JS的重要概念

### Scope 作用域

- var: function scope
- let: block scope
- const: 宣告一個唯獨的變數，作用域範圍跟let相同（不是全域！）

```js
function main(){
  var a = 1
  if(a==1){
    a=2
    var b=1 //b的範圍不是在{}內，而是在function內都是！
  }
  b=2
}
```

b的範圍在main(){}中

```js
function main(){
  let a=2
  if(a==1){
    let b=2
  }
}
```
a的範圍是main(){}，b的範圍是{}裡面


### Closure 閉包

- Closure一定是有兩層的function
- 如果要寫函式庫給別人用比較會用到畢包，但一般應用面還好。

```JS 有記憶的計算機
var i = 0
function MyFunc(){
  return {
    GetCount:function(){
      i++; return 1;
    }
  }
}
```

```JS 有記憶的計算機
function MyFunc(){
  var i = 0
  return {
    GetCount:function(){
      i++; return 1;
    }
  }
}
var o = myFunc() // 並得到 {GetCount()}
// 因為GetCount裡面有參考到i，所以外層的ｉ都會在
o.GetCount() ; 1
o.GetCount() ; 2
o.GetCount() ; 3
```


### 變數與常數

- var : function scope
  - 只在function內部存活
  - 如果在外面就會污染根物件
- let: block scope
  - 只在{ }內部存活
- const: block scope
  - 宣告一個`唯獨`的變數，作用域範圍跟let相同（不是全域！）

> 可以用let開發就不要用var

```js
wow = 1 
// window.wow = 1 但不會產生變數
```
```js
var wow = 1
// window.wow = 1 產生變數且污染根物件

```
```js
function main(){
  var a = 1
  if(a==1){
    a=2
    var b=1 //b的範圍不是在{}內，而是在function內都是！
  }
  b=2
}
```