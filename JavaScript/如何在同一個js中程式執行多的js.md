# 如何在同一個js中程式執行多的js

- 有時候會需要所有程式在同一個js中執行，這樣跑`npm run XX`比較方便

## 直接Require就好了

```js
//state.js
const mongoose = require('mongoose')
const state = require('../state')

mongoose.connect('mongodb://127.0.0.1/',{ useNewUrlParser: true, useUnifiedTopology: true })

const db = mongoose.connection

//各種程式碼
```


```js
//all.js
const createState = require('./state');
const createUser = require('./user');
const createDiagnosis = require('./diagnosis');
```