

# SOP

1. 確認需求
2. 簡單設計前端要呈現的資料
3. 建立SQL資料庫的表格schema
- 命名風格：id,c_id,teacher,start,end 
4. 整理過去資料（手清->自動清）
- [如何把2019-01-02T09:00:00+08:00轉時間？](時間語法.md)
> 如果前期自動化清資料的方法弄不好，拜託直接先丟到google sheet用手清，之後再用自動化，不要卡在這裡
5. 把資料import進資料庫	

# 常用技巧

## 如何把csv匯入google sheet

- 檔案-匯入-上傳csv－插入新工作表

## 如何利用google sheet 的 vlookup進行對照？（未來要去尋找Python的做法）

`vlookup(被查詢的字詞, 字典的範圍,2,FALSE)`

```s
=vlookup(B6,$F$2:$G$41 字典的範圍,2,FALSE)
```

## 如何在SQL中利用「特定列表」去搜索相關內容 in 

```sql
select * from `event` where name in -- 查查看事件中任何有課程A/課程B/課程C/課程D 的事件
(SELECT distinct(name) FROM `course`.classList) -- 一個列表 課程A,課程B,課程C,課程D
```

## 累積的問題？

如果編號長得像是
c01,c02,c03
f01,f02,f03
那可以mysql自動更新嗎？還是必須要輸入時就要自己資料要排好？