### 前後端驗證

- token：
  - 當POST帳號密碼到後端後，後端就會發一個token回來。
  - 當下次使用者要跟後端要數據時，就必須把token放在header當中送過去，否則會被拒絕。
  - token是可以設定期限的，可能是30min, 1hr, 幾天。
  - token是可以藏一些資訊的，例如：使用者名稱（可轉換成暗碼<->明碼）
  - token是無法被更改的，因為後段是前段的雜湊
- freshToken：
  - freshToken的作用是當token過期之後，就可以把freshToken送過去，後端會再送一個新的token跟fresh token回來。

情境：假設freshtoken期限是5天，token期限是1天。那在第二天發request給後端的時候，後端會發現token過期，所以不給資料。此時再送一次fresh token到後面，後端知道還在期限內，所以就會送一組新的token跟fresh token回來，然後fresh token的過期時間就會增長。

- cookie：
  - 一定會把


### Token 存在哪？

因為每次token都必須送到後端驗證才能拿到資料，所以前端就必須好好的儲存token，否則把token搞丟就沒東西可以送到後端。

常見的儲存方式如下：

- 存在localStorage：當網頁關閉重開後，token扔然會在localStorage裡面，所以header可以有東西可以送到後端。
- 存在sessionStrorage：當網頁刷新(refresh)之後，token扔然會在sessionStrorage裡面，所以header可以有東西可以送到後端。
- 存在變數裡面：但只要網頁刷新(refresh)之後，token就不見了，所以header沒有東西可以送到後端。


```js
localStorage.Authorization = 123
sessionStorage.Authorization = 123
// 可以直接在瀏覽器把sessionStorage開啟賦值
```
