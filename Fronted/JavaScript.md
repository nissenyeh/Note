# JavaScript

## Object destructuring

```Javascript
nissen = {
  name:'nissen',
  age:21,
  gender:2
}

const {name, age, gender}= nissen  // Mapping name has to be the same
```

## Array destructuring

```Javascript
var nissen = ['nissen',21,2]
var [nissen,age,gender]=nissen
```

```Javascript
console.log(name) //nissen
console.log(age) //21
console.log(gender) //2
```