### Promise


- axios 回來的資料會是Promise，必須用then去接
- 或者是使用await等待axios完成，才執行console.log


```js
  getB() {
    const APromise = axios.get('XXXX') // Promise {<pending>}
      .then((res)=>{
        console.log(res) // {data: Array(2), status: 200, statusText: "OK", headers: {…}, config: {…}, …}
      })
      .catch()
```

```js
  async getA() {
    const BPromise = await axios.get('XXXX') 
    console.log(queryRolesPromise)  // // {data: Array(2), status: 200, statusText: "OK", headers: {…}, config: {…}, …}
```

- 一次解析多的Promise

```js
    const APromise = axios.get(API.a);
    const BPromise = axios.get(API.b);
    const [AResponse, BResponse] = await Promise.all([APromise, BPromise]);
```