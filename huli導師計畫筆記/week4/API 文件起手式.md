# API 文件起手式
### 結構
1. url
2. 這支 API 的作用
3. 使用的 HTTP method、header 欄位
4. request body
5. response body

# Restful API
是一種 api 的型式風格，特色如下:
1. 有唯一的URL表示資源位置，統一的 API 接口。(Uniform Interface)
2. 無狀態。(Stateless)

以 API 而言，假設我們正在撰寫一組待辦事項的 API，
可能會有以下方式來作為 API 的 interface:

獲取使用者資料 /getAllUsers
獲取使用者資料 /getUser/1
新增使用者資料 /createUser
更新使用者資料 /updateUser/1
刪除使用者資料 /deleteUser/1

若是以 REST 風格來開發 RESTful API 的話:

獲取使用者資料 /GET /users
獲取使用者資料 /GET /user/1
新增使用者資料 /POST /user
更新使用者資料 /PUT /user/1
刪除使用者資料 /DELETE /user/1

兩者差異是在於 RESTful API 充分地使用了 HTTP protocol (GET/POST/PUT/DELETE)，達到:

以直觀簡潔的資源 URI
並且善用 HTTP Verb
達到對資源的操作
並使用 Web 所接受的資料類型: JSON, XML, YAML 等，最常見的是 JSON

###### tags: `week4` `RESTAPI`