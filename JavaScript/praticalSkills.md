# JavaScript

### Pratical Skills

## Object destructuring

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

console.log(mydata) // data
```

## Array destructuring

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

## Spread Operator 


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


