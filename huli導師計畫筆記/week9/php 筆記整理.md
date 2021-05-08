# php 筆記整理
1. GET / POST
- 前端必須用 form 來發出 get / post request 到 server 再轉給 php 檔案處理
- 所以我們可以利用 php 的 $_GET / $POST 來取得前端發出的值

2. 連線
- mysqli($serve_name, $username, $password, $dbname)
- -> 調用子程序(函數、參數)的方法
- empty() 查看回傳參數是否為空
- die() 出現錯誤訊息就停止並印出內容

3. 讀取 read
- 首先要利用 require_once() 把連線引用近來
- 接著用 $conn->query('MYSQL指令') 來對 db 下指令
- 取得資料後要把資料拿出來用 $result->fetch_assoc 來把資料擷取出來
[fetch_assoc 參考資料](https://richarlin.tw/blog/php-mysql-fetch/)

4. 插入 insert
- 首先先在畫面中新增插入的 input，並用 post method
- 接著開一個 insert.php 檔
- 第一個先檢查 post 是否為空
- 再來把取得的 post 資料設定為變數 $username
- 再利用 sprintf 把 sql method 另外設一個變數 $sql
- 接著就用 ->query('$sql') 來插入資料
- 最後再判斷有沒有成功 

5. 刪除 delete
- 首先要在 index.php 新增一個刪除按鈕，按鈕要能夠連結到 delete.php 並引用 id 當 querystring
- 接著新開一個 delete.php
- 在 delete.pho 中先判斷傳入的 $_GET　是否為空
- 接著照前面設定　$ID 及 $sql
- 接著用 ->query('MYSQL method') 來發出 delete 指令
- 最後用 .affected_rows = 1(true) 或 0(false) 來判斷是否刪除成功

6. 編輯 edit
- 首先在 index.php 新增一個表單附帶兩個輸入欄，按鈕要連結到 edit.php
- 接著新開一個 edit.php
- 在來判斷 post 的 id 及 username 是否為空
- 下面把引入的 id 及 username 各自設為變數 $id / $username
- 把要執行的 MYSQL method 設為變數 $sql
- 接著用 ->query($sql) 來發出 request
- 判斷 $result 是否為空

###### tags: `week9`