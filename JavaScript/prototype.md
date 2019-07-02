## Prototype Chain

- `__proto__` ： `__proto__` is the `property` which is taken from prototype

```js
var nissen = {
  name:'nissen',
  age:10
}

nissen.__proto__.nickname = "NiNi"

var Neo = {
  name:'Neo',
  age:30
}

console.log(Neo.__proto__.nickname) // NiNi

```

### Everything's  Prototype  is Object

- 物件的原型是「物件原型」
- 陣列的原型是是「陣列原型」，而「陣列原型」的原型是是「物件原型」
- Argements 的原型直接就是「物件原型」（所以他是類陣列）

![Alt text](/img/protoType.png)
