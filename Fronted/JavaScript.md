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

const {name, age, gender}= nissen  // Mapping name has to be the same
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