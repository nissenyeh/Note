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

## Sync修飾符：讓子層數據可以流向外層（父層）

- Prop只能讓父層資料傳進去子層，但是一但子層資料改變，父層資料不會變化(正常狀況下)
- `Sync`：
 - 透過`this.$emit(update:title, newTitle)` 可以把觸動父層的事件，把父層的數據做跟動

``` js 
// 父層
<pagination
  :total="total"
  :current-page.sync="currentPage"   //等同於 v-on:update:current-page.="doc.current-page. = $event"
/> 

```

``` js
// 子層
@Prop(Number) public currentPage!: number;

this.$emit('update:currentPage', newCurrentPage)

```

### 參考資料
 [Vue檔案：sync 修饰符](https://cn.vuejs.org/v2/guide/components-custom-events.html)
