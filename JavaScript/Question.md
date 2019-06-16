# 自我檢測


#### Q:請說明變數、物件、型別、屬性的定義與關係？

#### Q:請說明物件與型別的關係？

#### Q:請問 b.x的值為多少？
```js
var a = {x:1}
var b = a
a = {x : 2}
```
解答：1

詳解：

1. 建立1物件
2. 建立{x:1}物件，x屬性指向1物件
3. 建立a變數，{x:1}物件位置存到a
4. 建立b變數，{x:1}物件位置存到b
5. 建立2物件
6. 建立{x:2}物件，x屬性指向2物件
7. 把{x:2}物件的記憶體位置存到a

因為在以上過程中，b指向的依然是{x:1}，因此b.x=1

#### Q:過程中出現幾個變數、型態、物件


```js
var a;  
a = 1; 
a = "a";
a = "a" + a; 
```

- 曾經在記憶體中建立過幾個變數？ 
  - 解答：1
  - 詳解：建立了一個變數a

- 曾經在記憶體中出現過幾個型別？ 
  - 詳解：undefined、number、string

- 曾經在記憶體中出現過多少物件？ 
  - 解答：5
  - 詳解：程式碼運行如下
1. 宣告a變數，並把undefined物件位置指向變數a
2. 建立1物件，並把1物件位置指向變數a
3. 建立"ａ"物件，並把"a"物件位置指向變數a
4. "a" + a過程中把1轉換成"1"，建立一個"1"物件（不確定）
5. 建立"a1"物件，並把"a1"物件位置指向變數a

#### Q:請「閱讀」下面程式碼

```js
var a = 3
```

解答：
1. 建立一個3的物件
2. 建立一個a的變數
3. 把3物件的記憶體位置放到變數a當中 

#### Q:請問b.x 和 a.x 是多少？

```js
var a = {x:1}
var b = a 
a.x = a = {x:2}  
```
> a.x = a = {x:2}  
> {x:2} 的位置會同時被複製到a.x 跟 a 

解答：
b.x = {x:2} ; a.x = 2 

#### Q:請問a.x是什麼？

```js
var a = {x:1}
a.x = a
```
解答：a.a.a.a.a.a.a.a.a.............(循環參考）
詳解：參考自己是允許的！

#### Q:已知const表示唯讀，那下面程式合法嗎？

```js
const a = {}
a.name = 'will'
```
解答：可以，因為即使物件增加name的屬性，但a的記憶體都是一樣的。


#### Q:console.log(a.name)是什麼?

```js
var a = 1
typeof(a) // number
a.name = "will"
console.log(a.name) // 答案是 ??
```
解答： undefined

詳解：因為ａ指向物件1，而物件1不能擴增屬性，因此a.name是失敗的。

#### Q:console.log(a.name)是什麼?

```js
var a = 1 
Number.prototype.name = 2
a.name = 3
console.log(a.name)
```
解答：2

詳解：因為a.name只能是繼承來的，而不能是自己設定的。！

#### Q:練習題

```js
請依據以下範本撰寫一個 MyFunc 函式：
function MyFunc() {
// YOUR CODE HERE
}

撰寫完成後，必須可以正常執行以下程式碼：
var o = MyFunc();
console.log(o.Key1); // 回傳 1
console.log(o.Key2); // 回傳 2
```
解答：
```js
function MyFunc() {
  return {
    Key1:1,
    Key2:2,
  }
}
```
#### Q:練習題

```js
請依據以下範本撰寫一個 MyFunc 函式：
function MyFunc() {
// YOUR CODE HERE
}

撰寫完成後，必須可以正常執行以下程式碼：
var o = MyFunc();
console.log(o.GetA()); // 回傳值為 1
console.log(o.GetB()); // 回傳值為 2
```
解答：
```js
請依據以下範本撰寫一個 MyFunc 函式：
function MyFunc() {
  return {
    GetA:function(){ return 1}, 
    GetB:function(){ return 2 }
  }
}
```

#### 這段程式哪裡不好？

```JS
function test(a,b){
  c = a+ b
  return c
}
var d = test(1,2)
```
解答：c沒有宣告成區域變數，因此會汙染根物件
詳解：console.log(global.c) 會看到 c = 3，如果希望d也不要污染到根物件，可以用IIFE包裹住。



### ES6語法糖練習

#### Q:不透過concat的方式，把兩陣列進行合併

```js
var a = [1,2,3]
var b = [4,5,6] 
```

解答：var c = [a...,b...]

#### Q:其餘參數：只回傳1,2，其他參數用陣列回傳

```js
f(1,2,3,4,5,6)
```

解答:

```js
function fc(a,b,...args){
  return a,b,args
}
```

#### Q:解構賦值-簡化下面的程式

```js
var arr = [1,2,3]
var a = arr[0]
var b = arr[1]
var c = arr[2]
```
解答:
```js
var arr = [1,2,3]
var [a,b,c] = [1,2,3]
// var a,b,c = [a,b,c] = [1,2,3]
```
