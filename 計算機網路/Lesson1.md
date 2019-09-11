
### 計算機網路

網際網路基本是有多層組合，大致可以分為以下幾層

- Application Layer：

- Transport Layer：`TCP`就是屬於Transport Layer的一個元件，可以
  1. 保證資料可以送到對方那邊
  2. 藉由下降提升來控管網路速度

- NetWork Layer：有點像是郵局，會把資料轉來轉去Data forwarding and routing

- Data Link Layer

- Physical Layer

### 網際網路的樣貌 = 核心網路（ISP） ＋ 邊緣網路（使用者）

在網際網路中，一般的使用者基本是在網路當的邊緣當中，而中間的核心則是由ISP提供的`核心網路（Networkcore）`進行有線串連。在邊緣網路的資料會先在區域中把資料彙集到一個路由（Router），再一起送出去到核心網路（Networkcore）中

> ISP（Internet Service Provider，簡稱ISP）：意思是網路服務的提供者，例如：中華電信

### 主機(Host)是什麼？

只要是連結網路的末端設備(end system)都可以叫做host（例如：PC、Server、phone）



### 頻寬(bandwidth)是什麼？

指訊號所占據的頻帶寬度，通常頻寬(bandwidth)愈大網速有機會愈高（但不保證）。去ISP購買服務時，要注意他的「頻寬」是專屬頻寬還是共享頻寬。如果是共享頻寬，可能會有很多人一起用，所以也不會很快。

### 路由（Router）是什麼?

路由（Router）是一個資料集散地，像是家裡的設備會把資料會聚到Router再送到核心網路（Networkcore）中。



### 封包(Packet)是什麼？

在網路中，資料通常不是一次送，而是切成許多的封包（封包）。