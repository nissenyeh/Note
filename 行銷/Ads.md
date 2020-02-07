# Google Ads

- UTM是什麼？

UTM（Urchin Tracking Module）簡單來說就是一個追蹤的方式，他在網址的後面加上不同參數，即使連到同一個網址，工具也可以知道他的來源。

`http://www.campaign.com?utm_source=facebook`
`http://www.campaign.com?utm_source=campaign`

1. `utm_source`表示廣告活動來源。用以表示為你帶來流量網站或是來源，比方說Google搜尋引擎、臉書、電子報。
如：utm_source=google, utm_source=facebook
2. `utm_medium`表示廣告活動媒介。表示行銷或廣告的媒介，如：單次點擊出價CPC、聯播網廣告、電子報。
如：utm_medium=cpc, utm_medium=newsletter
3. `utm_campaign`表示廣告活動名稱，主要是為了辨別廣告活動的形式，如官方網站或是促銷的商品、活動名稱、促銷代碼、廣告標語。
如：utm_campaign=cybermonday_promotion
4. `utm_term`表示廣告活動字詞，通常是Google付費關鍵字廣告所使用的字詞。
如：utm_term=baby_sling
5. `utm_content`表示廣告活動內容，通常用於辨識A/B測試的指定內容廣告活動，表示連到同一個網址的不同廣告或是連結的成效。
如：utm_content=textlink, utm_contetnt=600px_banner

# ValueTrack

目的：下廣告的時候，不只增加流量，也可以分析使用者的數據（用什麼設備之類的）

重要參考網址：
- [不同的參數](https://support.google.com/google-ads/answer/6305529?hl=zh-Hant#ttdsa)
- [最終到達網址尾碼](https://support.google.com/google-ads/answer/9054021?hl=zh-Hant)
- [什麼是追蹤範本](https://support.google.com/google-ads/answer/6273460?hl=zh-Hant)


```
{lpurl}?utm_device={device}&keyword={keyword}&matchtype={matchtype}
```

Exp:

- 若點擊來源為行動裝置，您會看到：
http://www.example.com/?device=m

- 若點擊來源為平板電腦，您會看到：
http://www.example.com/?device=t

- 若點擊來源為桌機或筆電，您會看到：
http://www.example.com/?device=c



- GA是否可以解析utm_device，是否可以解析關鍵字？
