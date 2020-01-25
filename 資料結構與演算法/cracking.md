# crack the coding interview

## Ch1

- 大公司想看problem-solving的能力，基礎的演算法可以看得出來
- 大公司不會介意部分優秀的人才因為沒練習演算法，而錯過他們。他們寧願有good enough的員工。
- 白板面試可以容許一些小的語法錯誤，重點是邏輯是否通順。
- 面試是一個面試官比較的過程，所以遇到難的問題不一定是壞事。

###  Microsoft Interview 

- 白板題
- 一定要準備 "Why do you want to work for Microsoft?" ，因為他們想找對科技有熱情的人。
- Microsoft給不同的團隊自己的控制權，因此這導致評估標準有些許不同。

### The Facebook Interview

- Behavioral：Facebook希望有熱情的人，因此會問一些價值觀。
- Coding and Algorithms：標準編碼和算法問題

###  The Google Interview

-  google面試會從first phone screen開始，可能會解一些困難的題目吧（？）
- 在on-site interview會有四到六个人，其中一個是lunch interviewer。每次的面試反饋都會對其他面試官保密，因此可以放心，每次的面試都可以當作一次的空白。
- interviewer可以根據自己的想法進行面試，書面反饋意見將提交給工程師和經理的僱用委員會（HC）， 反饋通常分為四類（分析能力，編碼，
經驗，溝通），您的總分從1.0到4.0。而HC通常不會是你的面試官
- HC希望看到至少一位“enthusiastic endorser”的面試官，因此得分分別為3.6、3.1、3、1和2.6的數據包要優於所有3,1。您不一定需要在每次面試中都表現出色，並且phone screen performance通常並不是最終決定的重要因素。
- 必要準備：Google很關心如何設計scalable system的系統。 所以，請確保您做好準備System Design and Scalability，並且不論經驗都相當重視analytical (algorithm) skills。
- 面試官不會做出雇用的決定，而是提供反饋讓HC決定。

### 給外國人的建議

有些公司會因為錯字而丟掉您的簡歷。 請至少獲得一種母語
者校對。此外，在美國不要提供年齡，婚姻狀況或國籍相關內容， 公司不喜歡這種個人信息，因為這會給他們帶來法律責任。

### 準備建議

- learn and master BigO
- Do several mock interviews
- Continue to practice interview questions.
- Create list to track mistakes you've made solving problems. 
- Form mock interview group with friends to interview each other. 

# BigO

- BigO是一個非常重要的概念，您了解會被嚴厲地評判為
不太了解0，也很難判斷算法何時變快或慢點。

- 小題目：您的硬盤上有文件，需要將其發送給您在遠方的朋友，該怎麼辦？您需要盡快將文件發送給您的朋友。您應該如何發送？文件小可以用電子郵件，文件真的很大（超過天才能傳輸），通過飛機去送可能更快。

- `Time Complexity的概念`
   - O(s)：時間根據size大小而不同（就像用電子傳輸去送郵件）
   - O(1)：時間不會根據size大小而不同，時間是恆定的（就像開飛機去送郵件）


## Best Case, Worst Case, and Expected Case 

對於每個runtime都可以用Best Case, Worst Case, and Expected Case 來形容

以`quicksort`來說，quicksort是讓一個隨機的數字當作pivot，然後把其他數值往左丟或是往右丟，然後左右側的值都用類似的方式處理。

- `Best Case`: 每個數字都同一個值，所以分一次就沒事了，因此複雜度是0（N）。

- `Worst Case`: 每次挑到的random值都挑到了最大或是最小的，所以下一輪還是從頭開始，因此複雜度是0（N^）。
- `Expected Case`: 正常情況下應該是「有時候挑得好，有時候挑得不好」，因此我們期待複雜度大約落在0（N log N）。


很少討論最佳情況下的時間複雜度，因為這不是一個非常有用的概念。 畢竟，因為基本上採用任何算法，在最佳情況下都可以獲得0(1)時間。

對於許多算法，`Worst Case`和`Expected Case`是相同的。 但是有時它們是不同的。

# Space Complexity 

從p.52開始看


# 如何準備case

- 嘗試自行解決問題，並務必考慮空間和時間效率
- 將code寫在紙上，習慣用紙來寫程式
- 在紙上測試您的代碼。這意味著要測試general cases, base cases, error cases等。您在面試時需要這樣做，因此最好事先進行練習。
- 將您的書面代碼原樣輸入計算機。您可能會犯很多錯誤。列出全部您所犯的錯誤，以便您可以在精算面試中牢記這些錯誤。

嘗試進行盡可能多的模擬採訪。您和朋友可以輪流互相進行模擬面試。儘管您的朋友可能不是專家面試官，但他或她仍然可以引導您解決編碼或算法問題。

## Core Data Structures, Algorithms, and Concepts

- 大多數面試官不會詢問有關binary tree balancing or other complex algorithms。 坦白說，由於離開學校好幾年，他們可能也不記得這些算法。
通常只要求您了解基本知識。 以下絕對必要知識的列表：

Data Structures：
- Linked Lists
- Trees, Tries &Graphs
- Stacks & Queues 
- Heaps 
- Vectors/ArrayLists
- Hash Tables 

Algorithms:
- Breadth-First Search 
- Depth-First Search
- Binary Search
- Merge Sort 
- Quick Sort 

Concepts
- Bit Manipulation 
- Memory (Stack vs. Heap) 
- Recursion 
- Dynamic Programming
- Big 0 Time & Space 

對於以上每個主題，請確保了解如何使用和實現它們，並在知道什麼情況適用，還有他的space and time complexity，並練習實現數據結構和算法（在紙上，然後在計算機上）。特別是` hash tables`是非常重要的主題，確保你很了解這個資料結構。

