# this

### Question

```js
var obj = {
  print: function(){
    console.log(this)
  }
}

var stolenFunction = obj.print
obj.print() // this -> object { print: [Function: print] }
stolenFunction() // this -> `window`
```
Please explain why the values of the last two lines of the function are different ?

### All function is `func.call(environment, p1, p2)`

 `func.call(environment, p1, p2)` is normal way to call function

so: 

- `obj.print()`  is equal to `obj.print.call(obj)`
- `print()`  is equal to `print.call(window)`

Example:

```js

obj.print.call(window) // window
obj.print.call(obj) // obj
```

If the context you pass is null or undefined, then the window object is the default context (the default context in strict mode is undefined)

```js
obj.print.call()  // window, not obj
```

## What is `this`

 `func.call(environment, p1, p2)`

> this = environment 

## Reference

- [this 的值到底是什么？一次说清楚](https://zhuanlan.zhihu.com/p/23804247)