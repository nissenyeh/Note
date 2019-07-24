# JavaScript

### Pratical Skills

## Object destructuring 物件解構

- Mapping name must to be the `same`

```Javascript
nissen = {
  name:'nissen',
  age:21,
  gender:2
}

const { name, age, gender }= nissen  // Mapping name has to be the same
```

- It's helpful for getting specific data from object

```Javascript
response = { data: {…}, status: 200, statusText: "OK", headers: {…}, config: {…}, … }

const { data: mydata } = response // If  don't want the origin name from object ,renameing is avaliale.


const { data: mydata } : { data: string} = response // if you want interdace, that's fine

console.log(mydata) // data
```

## Array destructuring 陣列解構

- Mapping name `doesn't have to` be the same

```Javascript
var nissen = ['nissen',21,2]
var [nissen,age,gender]=nissen
```

```Javascript
console.log(name) //nissen
console.log(age) //21
console.log(gender) //2
```

## Spread Operator 展開運算子


```JavaScript
var a = [1, 2, 3]
var b = [...a]  // [1,2,3]
```

```JavaScript
var x = {
  a:1,
  b:2
}
var y = {  // y doesn't use same memory address with x object 
  ...x
}

var z = x  // z use same memory address with x object 

console.log(y==x,z==x) // false , true
```

## Mapping without `IF`

``` JavaScript
// IF style
var word 
if(word == 'a'){
  word = 1
}
else if (word == 'b'){
  word = 2
}
else if (word == 'c'){
  word = 3
}
```


``` JavaScript
// Object style
const dicitionary = {
  a:1,
  b:2,
  c:3
}

var word = 'a' // a
dicitionary[word] // 1
```

## Arr Function 箭頭函式

```JS
var f = function a() {
  return 43
}
```
```js
var f = () = > {return 43} //要記得，需要return
var f = () = > 43 // 預設會return
```

```js
// Eslint
const inserted = arr.some(item => item.id === rf.id); //第一個參數不用括號，不用return 

const position = arr.findIndex((item, index) => item.id > rf.id); // 兩個參數才要括號，不用return 
```

### default parameters 預設參數

```js
var a = function(a,b=3){
  return a+b
}
```

### Rest parameters 其餘參數

- Put rest parameters in the array

```js
function f(a,b,...args){
  return args
}
f(1,2,3,4,5,6) // [3,4,5,6]
```