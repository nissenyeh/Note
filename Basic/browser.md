# 瀏覽器的流程

1. 透過HTTP協議，向server獲得HTML程式碼。
>得到像是這樣的東西
```html
<!DOCTYPE html><html lang="en"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0"><link rel="stylesheet" href="//at.alicdn.com/t/font_137970_p1tpzmomxp9cnmi.css">...
```
- HTTP協議是基於TCP出現的一種純文本協議
  - TCP：屬於底層的通訊協議，規定了`數據傳輸和連接的規則`，是一個雙向的訊息通道。
  - HTTP：是基於TCP的基礎上應用協議，規定了`傳輸的內容規範`，是由Request-Respond的形式。

```
telnet google.com 80  //建立TCP連接，但這個時候沒有
```

```
GET / HTTP/1.1   // request line
Host: time.geekbang.org
```

```
HTTP/1.1 301 Moved Permanently
Date: Fri, 25 Jan 2019 13:28:12 GMT
Content-Type: text/html
Content-Length: 182
Connection: keep-alive
Location: https://time.geekbang.org/
Strict-Transport-Security: max-age=15768000

<html>
<head><title>301 Moved Permanently</title></head>
<body bgcolor="white">
<center><h1>301 Moved Permanently</h1></center>
<hr><center>openresty</center>
</body>
</html>

```

2. 瀏覽器將HTML代碼解析成DOM樹

3. 計算DOM上的CSS屬性
4. 根據CSS 屬性對元素逐個進行渲染，得到內存中的位圖
5. 合成之後，再繪製到界面上。

