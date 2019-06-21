## Constructor

### Function constructor


```JS
function rooms(){
  this.height = 200
  this.width = 300
  this.measure = function(){
    return this.height * this.width
  }
}
```

```Js
const rule = new rooms()
console.log(rule) //rooms { height: 200, width: 300, measure: [Function] }
console.log(rule.measure)  // [Function]
console.log(rule.measure())  // 60000
```

`const rule = new rooms()`

1. `new`: Create a empty object
2. `this`: this refers to the new object

### Class constructor


- `get` -> set a property

```JS
class rooms {
  constructor() {
    this.height = 200
    this.width = 300
  }
  get getMeasure() {
    return this.height * this.width;
  }
  measureMethod() {
    return this.height * this.width;
  }
}
```

```JS
const rule = new rooms();
console.log(rule) // rooms { height: 200, width: 300 }
console.log(rule.getMeasure) // 60000
console.log(rule.getMeasure()) // is not a function
console.log(rule.measureMethod) // function
console.log(rule.measureMethod()) // // 60000
```

### Object

- this -> refer to the room()
```JS
var room = {
  height: 200,
  width: 300,
  measure:function() {
    return this.height * this.width
  }
} 
console.log(room.measure()) // 60000
```


- this -> refer to the global

```JS
var stolenFunction = room.measure
console.log(stolenFunction())   //NAN
```