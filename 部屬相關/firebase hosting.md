### 概要
在 [firebase](https://console.firebase.google.com/u/1/) 可以建立專案部屬靜態網站、連結資料庫甚至擁有 https 連線。

### 步驟
1. 首先進入目標資料夾建立 npm
2. `npm install -g firebase-tools`
3. `firebase login` 登入 google 帳號後，會直接連接 firebase acount
4. `firebase init` 會一步一步建立 firebase 的基礎環境，包含 `firebase.json` 及一個 `public` 的資料夾，後續要把所有靜態網站的 source 放在資料夾中
5. `firebase deploy` firebase 會問要建立的專案名稱及 app name ，後續可以在 firebase 管理頁面中看到
6. 網域轉址要"新增自訂網域"，firebase 會給你驗證的 txt 內容，至 DNS 服務商新增一個 txt 區域檔並貼上內容，驗證結束後 firebase 會給你相對應的 ip 位址就可以在 DNS 服務商建立 A紀錄轉向了。
![](Pasted%20image%2020210509125011.png)
![](Pasted%20image%2020210509124935.png)

### reference 
[[教學] Firebase Hosting 免費1G/10G靜態網頁空間架設，與綁定網域名稱](https://www.minwt.com/website/server/21596.html)