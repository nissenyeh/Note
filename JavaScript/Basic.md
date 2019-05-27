# Basic 


1. `by reference`: Object (e.g: object, array) 
> array is a kind of JS object!
2. `by value`: Boolean, Null, Undefined, Number, String

```JavaScript
var arr = [1, 2, 3]
var newArr = arr[0] = 0
console.log(arr)  // [0, 2, 3]
```