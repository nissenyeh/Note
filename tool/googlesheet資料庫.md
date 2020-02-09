# 以 Google Sheet 為資料庫做自己的API

- 使用一個叫做[tabletop.js](https://github.com/jsoma/tabletop)的套件

1. 開啟google sheet
    - 在sheet上面的`File`選擇`Publish to the web`（即使連結用不到，好像也一定要做這個步驟）
    - 使用共享並選擇`Anyone with a link`
    - 把連結貼到`publicSpreadsheetUrl`中

2. 獲取google sheet資料（以資源申請系統為例）

```js
import Tabletop from 'tabletop'

Tabletop.init( 
    { 
        key: this.publicSpreadsheetUrl,
        callback: this.dataParser,
        simpleSheet: false 
    }
)

dataParser(data, tabletop) {
    arr = []
     // 獲取不同sheet的資料

    var sheet1 = data['sheet1'].elements 
    var sheet2 = data['sheet2'].elements
    var sheet3 = data['sheet3'].elements
    var sheet4 = data['sheet4'].elements
    // 合併不同sheet的資料  
    var arr = arr.concat(sheet1, sheet2, sheet3, sheet4); 
    // 製作自己的API
    this.resource = arr.map((item, index)=> {
        return { 
            category: item['資源類型'],
            title:item['名稱'],
            qualifications:item['申請資格'].split("/"),
            applyDeadline:item['申請期限'],
            announceDeadline:item['預計結果通知日期'],
            number:item['剩餘數量'],
            supplier:item['提供者'],
            source:item['資源來歷'].replace(/\n/g,'<br/>'),
            description:item['描述'].replace(/\n/g,'<br/>'),
            attachedMission:item['附帶任務'].replace(/\n/g,'<br/>'),
            referenceLink:item['參考連結'],
            photo:item['照片'],
            applyWay:'寄信至',
            applyLink:item['表單連結'],
            applyMission:item['申請注意事項']
        } 
    }).sort(function (a, b) {
        return new Date(a.applyDeadline).getTime() - new Date(b.applyDeadline).getTime() 
    });
},
```

3. 完成自己的API!


## 字串換行的處理

google sheet的換行會是`\n`，把它用`<br/>`取代掉

```js
string.replace(/\n/g,'<br/>'),
```