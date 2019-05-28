# Prop and $emit

## 父層傳入變數、啟動函式的方法
  - `:customname = "fatherData"`  把fatherData傳到子組件中，然後子組件可以用@prop把customname把資料接起來
  - `@customFunction = "fatherFunction"` 當customFunction在子組建被emit的時候，就會啟動裡面的fatherFunction函式

```Js
<template>
  <div>
    <childern
      @customFunction="response"
      :customname="ask" />
    <div>{{ responseText }}</div>
  </div>
</template>

export default class App extends Vue {
  ask = 'who are you'
  responseText = ''
  response(value:any){
    this.responseText =  value
  }
}
```

## 子層承接變數、向外啟動函式的方法
  - `@Prop(String) customname!: string` 可以把父層傳進來變數接下來
  - `this.$emit('change', this.response)` 可以把父層的函式啟用，並把`response`傳到外層

``` Js
<template>
    <div> 提問：{{ customname }}</div>
    <button on-click="responseTalking">要求回條</button>
</template>

export default class childern extends Vue {
  @Prop(String) customname!: string;

  response = '回條'

  responseTalking(){
    this.$emit('customFunction', this.response)  // 可以把變數傳到父層
  }
```