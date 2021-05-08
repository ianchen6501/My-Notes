# 資料庫正規化 及 資料庫關聯(SQL JOIN)
### 定義
避免依賴性、重複性並建立主鍵(primary key)
[DRAWSQL](https://drawsql.app/templates/koel)

### 資料庫關聯(SQL JOIN)
所以其實我們可以在 SQL 中設定一個欄位彼此關聯，當設定關聯後會出現一個表單，顯示關聯的部分，因為不一定每一筆都可以關聯，所以當然也可以設定聯集、交集等特性(例如: [visual join](https://joins.spathon.com))，裡面就列出了
> inner join
> left / right join
> outer join
這些實際在 SQL 的語法如下：
``SELECT * FROM Ian_comments left join Ian_users ON Ian_comments.username = Ian_users.username``

###### tags: `week11`