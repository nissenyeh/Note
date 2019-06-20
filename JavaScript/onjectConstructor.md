### New

### Create a Object

#### Function constructor

```JS
function rooms(){
  this.height = 200
  this.width = 300
  this.measure=function(){
    return this.height*this.width
  }
}
```

```Js
const rule = new rooms()
console.log(rule) //rooms { height: 200, width: 300, measure: [Function] }
console.log(rule.measure)  // [Function]
console.log(rule.measure())  // 60000
```

#### Class constructor


- `get` -> set a property

```JS
class rooms {
  constructor() {
    this.height = 200
    this.width = 300
  }
  get measure() {
    return this.height * this.width;
  }
}
```

```JS
const rule = new rooms();
console.log(rule) // rooms { height: 200, width: 300 }
console.log(rule.measure) // 60000
console.log(rule.measure()) // 60000
```

#### Object

- `this` - > the environment which run function

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
```JS
var stolenFunction = room.measure
console.log(stolenFunction())   //NAN
```