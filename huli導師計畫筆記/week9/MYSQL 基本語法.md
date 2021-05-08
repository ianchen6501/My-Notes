# MYSQL 基本語法
### Select
可以 select 不同欄位、值的內容
```sql=
SELECT id as name from 'table' 
--用 as 可以變更顯示出來的欄位名稱
SELECT id as name from 'table' WHERE id = 1
-- where 用來設定查詢的欄位設定條件
SELECT id as name from 'table' WHERE id = 1 and content = ''
-- 可以用 and 來設定多重條件，注意 string 要用 " 包裹
SELECT id as name from 'table' WHERE id = 1 or content = ''
-- 也可以用 or 來查詢符合其中之一的值
-- select 條件也可以用數學式或邏輯符號表式
```

### INSERT
```sql=
INSERT INTO `測試資料表`(`id`, `time`, `content`) VALUES ([value-1],[value-2],[value-3])
```

### UPDATE
```sql=
UPDATE `測試資料表` SET `id`=[value-1],`time`=[value-2],`content`=[value-3] WHERE 1
-- 要注意 where 一定要加不然就會整個 table 的資料都被變更
```

### DELETE
```sql=
DELETE FROM `測試資料表` WHERE 0
--要注意的是一些比較重要的資料其實沒有真的被刪除，而是被加入一個 'is_deleted' 的 tag 讓他之後消失在眾人眼前
```

###### tags: `week9`

