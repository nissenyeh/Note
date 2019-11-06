# RDT 可靠資料傳輸(Reliable Data Transfer)

在理想的TCP模型中，我們會假設訊息在網路上會安全的運送。但現實並非如此，傳輸協定的下層是「不可靠」，可能存在著許多像是錯誤、封包遺失等等狀況，因此這時候，我們就必須在傳輸層自行設計一些溝通模型，來確保sender和receiver的溝通是正確的，如果正確要讓sender送下一個檔案，如果錯誤要讓sender重送檔案。而這樣的溝通模型就稱為「可靠資料傳輸(Reliable Data Transfer)」。通常狀況下，RDT的模型是用FSM(Finite State Machine 有限狀態機)來定義狀態與操作方式。


## rdt1.0

主要有傳輸端與接收端兩個部分，資料傳輸方式很單純，傳輸端等待上層傳資料進來，收到上面的資料

以後裝成封包送出去。
接收端收到封包以後，將封包解開，把訊息往上送。

## rdt2.0

sender會送封包到receiver

- 當receiver收到資料，會回傳一個ACK（表示Acknowledgement），這時候sender就知道對方有收到了。
- 當reveiver收到錯誤的資料，會回傳一個NAK（Negative-Acknowledgment），這時候sender就知道要再送一個。
- 當reveiver沒有收到資料（rdt2.0 沒有機制處理這個狀況）
- 當receiver收到資料，會回傳一個ACK（表示Acknowledgement），但是沒有送到（rdt2.0 沒有機制處理這個狀況）
- 當receiver收到資料，會回傳一個NAK（Negative-Acknowledgment），但是沒有送到（rdt2.0 沒有機制處理這個狀況）
- 當receiver收到資料，會回傳一個ACK（表示Acknowledgement）和checksum，但是壞掉了
- 當receiver收到資料，會回傳一個NAK（Negative-Acknowledgment）和checksum，，但是壞掉了


息，當資料接收到以後確認無誤，會送ACK給來源已確定資料無誤。當偵測到錯誤時 會傳回NAK通知來源

端再送一次。

## rdt2.1

改版：在2.1版中新增了sequence number去確定是否傳遞了一樣的封包

同樣使用ACK與NAK來確認訊息，封包的號碼可以用來確認是否重新傳輸封

包。
例如接收端在等待編號0的封包，結果收到封包1，此時會回傳ACK1給來源端，而正在等候ACK0的來源端

收到ACK1 表示封包0可能遺失，所以會再重送封包0。


## rdt2.2

改版：在2.2版中，取消NAK，直接用把ACK加上一個bit的sequence number去表示ACK和NAK
- ACK 0 表示 ACK
- ACK 1 表示 NAK


## rdt3.0

改版：在3.0版中，sender增加了timer，去處理資料不見的問題。TCP會根據前一次的運送狀況，去稍微統計下一次timer應該設定多長。

sender會送package0到receiver
- 當receiver收到資料，會回傳一個ACK0，這時候sender就知道對方有收到了，然後它再送package 1 到receiver（0和1交替）...
- 當reveiver收到錯誤的資料，會回傳一個ACK1，這時候sender就知道要再送一個。
- 當receiver收到資料，但sender以為沒收到，它就在重送package 0 ，之後sender接續收到兩個ACK0，他就把重複的ACK丟掉了。
- 當reveiver沒有收到資料，sender等了一下發現沒有回應，它就在重送package 1（如果超過default 7次就不送了）
- 當receiver收到資料，會回傳一個ACK0，Sender如果等了一個合理的時間，但是沒有收到東西，就會重送package0，receiver檢查了sequence number知道這是重複的，所以就就把它丟掉，並且再回一個ACK0。
- 當receiver收到資料，會回傳一個ACK1，Sender如果等了一個合理的時間，但是沒有收到東西，就會重送package0。
- 當receiver收到資料，會回傳一個ACK0和checksum，但是壞掉了
- 當receiver收到資料，會回傳一個ACK1和checksum，，但是壞掉了

random lost：隨機遺失，不知道為什麼就消失
congestion lost：堵塞遺失，網路塞爆，送100次都送不到

## Pipelining Protocols 是什麼？

實際的情況下並不是
sender送出package -> sender等待receiver的ACK ->sender再送出下一個package
因為這樣中間會有很多等待時間

實際的情況下比較像是
sender連續送出一堆package -> receiver如果確認收到package就連續送出一堆ACK ->sender連續收到一堆ACK

那這就稱為`Pipelining Protocols`

### Pipelining Protocols 的類型

1. Selective Repeat：

假設sender送出1~10的package，而receiver只缺少9，那他就發一個NAK去sender讓他把9送過來。那這樣的好處就是，他可以只去拿需要的資料，而不需要一次讓sender送很多。但缺點就是，他必須有buffer去把1~8和10放好，然後管理當中的順序問題。

2. Go-back-N：

假設sender送出1~10的package，而receiver只缺少9，那他就發一個NAK(9)去sender讓他把9~9+N送過來。那這樣的好處就是，可以照順序去收，不需要buffer去把1~8和10放好，但壞處可能就是sender需要常常送重複的內容。

- sender：sender一次送出0~N個package到receiver那邊，receiver收到後就會告訴sender所謂的cumulative ACK。假設是5好了，那就表示receiver收到了1~5的package對方都收到了。那sender就會送6~6+N個package。那假設0的timer過期了，那sender就會重新送0~N個package。
- receiver：當receiver收過0了，他會預期他要收到1的package，如果沒有（像是收到5)，那他就會把5丟掉，然後一直回0的ACK到sender那邊，讓sender把1~1+N送過來。