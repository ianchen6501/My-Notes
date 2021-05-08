# 留言板 DIY 
### 架構
db table:
1. users - id / username / password / nickname / created_at
2. comments - id / username / comments / created_at
3. tokens - id / username / token / created_at

畫面:
1. 主畫面(顯示留言)
2. 登入畫面
3. 註冊畫面

php function:
0. conn
1. register
2. login
3. logout
4. add-comment

utils:
1. rand()
2. getUsersfromUsername()

steps:
1. 建立資料庫 table
2. 建立連線功能
3. 建立註冊功能
4. 建立登入功能(session)
5. 建立登出功能
6. 建立留言功能

###### tags: `week9`