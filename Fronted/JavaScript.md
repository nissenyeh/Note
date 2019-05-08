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

- It's helpful for getting specific data from object

```Javascript
response = {data: {…}, status: 200, statusText: "OK", headers: {…}, config: {…}, …}
const {data} = response
```

- If you don't like origin name of object , renameing is avaliale!

```Javascript
response = {data: {…}, status: 200, statusText: "OK", headers: {…}, config: {…}, …}
const {data:mydata} = response
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