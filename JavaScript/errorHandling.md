# Error Handling

### Try catch

- `try`: statement will keep running `until error happens` try裡面的程序會持續執行，直到發生了錯誤而被中斷並因此跳到catch
- `catch`: statement will run if and only if try has error   一但`try`發生錯誤，就會直接跳到catch裡面
- `throw`: statement throws a user-defined exception. 自製的錯誤訊息

```JavaScript
try {
  console.log('run：會執行')
  bug()  // a error happens  
  console.log('dont run：不會執行')  // directly go to catch and it doesn't console 'dont run' 
} catch(error){
  console.log(error)  // ReferenceError: bug is not defined 
}

// run
// ReferenceError: bug is not defined
```

```JavaScript
try {
  console.log('run：會執行')
  try{
    console.log('run：會執行')
    bug();
    console.log('dont run：不會執行')
  }
  catch(innerError){
    throw(innerError)
  }
  console.log('dont run：不會執行')
} catch(outerError){
  console.log(outerError)  // ReferenceError: bug is not defined
}

// run
// run
// ReferenceError: bug is not defined
```