# 以 Google Sheet 為資料庫做自己的API

主要使用[tabletop.js](https://github.com/jsoma/tabletop)的套件

1. 開啟google sheet
    - 在sheet上面的`檔案`選擇`發佈到網路`（即使連結用不到，好像也一定要做這個步驟）
    - 選擇`共用`並選擇`知道連結的人均可以檢視`
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

```json
0: {category: "物資", title: "【書籍】西恩．德維尼↵《林書豪精神－堅毅》", qualifications: Array(2), applyDeadline: "-", announceDeadline: "-", …}
1: {category: "物資", title: "【家電】家樂福小家電", qualifications: Array(3), applyDeadline: "2020/1/17 23:59:00", announceDeadline: "2020/1/30 18:00", …}
2: {category: "課程企劃", title: "免費 6 個月VoiceTube APP Pro 付費等級帳號", qualifications: Array(4), applyDeadline: "2019/9/29 23:59", announceDeadline: "2019/10/15 18:00", …}
3: {category: "課程企劃", title: "哿哿設計-美術課教案x桌遊合作", qualifications: Array(3), applyDeadline: "2019/12/22 23:59", announceDeadline: "-", …}
4: {category: "專業協助", title: "領導力教練(Coach)會談", qualifications: Array(2), applyDeadline: "2019/09/17 18:30", announceDeadline: "2019/10/17 18:30", …}
5: {category: "經費", title: "測試資料", qualifications: Array(1), applyDeadline: "2020/01/05", announceDeadline: "", …}
```


## 字串換行的處理

google sheet的換行會是`\n`，把它用`<br/>`取代掉

```js
string.replace(/\n/g,'<br/>'),
```