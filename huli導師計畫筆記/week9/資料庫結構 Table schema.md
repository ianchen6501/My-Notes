# 資料庫結構 Table schema
### table 
資料庫的表，會有不同的結構如下

1. table 名稱: 
2. 欄位名稱: 如 id
3. 型態: 欄位儲存資料的型態，要考量儲存的內容複雜度(如儲存分數可用 tinyint) int / tinyint / date / char / varchar / text / tinytext ...
4. 長度/值: 資料的長度
5. 編碼: 
6. 預設值:
7. 編碼與排序: 可不選，會採用 table 的設定，table 沒有設定就會採用 database 的設定
8. 屬性: unsigned = 不顯示負數
9. AI: auto increment 自動增加，讓 id 不會重複

資料庫設定好就可以儲存建立，建立後就可以新增移除資料。

### 主鑑 primary key
就是該 table 最主要的 key 

### 唯一 unique
內部資料不得重複，primary key defalt 會是 unique

### 索引 Index
有點像是 hackmd 的索引，幫助之後查索資料，但會佔據部分空間，索引可以多個欄位一起建立索引






###### tags: `week9` `table schema`