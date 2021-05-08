### fb 登入流程
用戶在你的網站決定要用facebook登入->跳出對話框詢問客戶是否同意讓app存取資料或是做其他動作->客戶同意後facebook給app access token，app就可以使用token來做事了。

### 插入 sdk


### 檢查登入狀態

### 新增登入/登出按鈕


### 調整 app 隱私權政策
原本的 fbapp 隱私權政策為 "調整中"，需要另外設定，這邊透過 [privacyPolicy](https://app.privacypolicies.com) 來建立一個專屬的隱私權網址。
建立完成後再回到 fb app 的基本資料裡面輸入網址，輸入隱私政策網址，並點擊 "調整中"，送出後會變成 "上線中"

### 輸入資料刪除回呼(非必要)
當使用者要求要刪除資料時，系統會呼叫資料刪除回呼

[privacyPolicy_w22_blog](https://www.privacypolicies.com/live/458ad15a-086e-47ca-b958-48ea76aca6e6)


### reference
[React + Facebook - How to use the Facebook SDK in a React App](https://jasonwatmore.com/post/2020/10/28/react-facebook-how-to-use-the-facebook-sdk-in-a-react-app)
[如何在網站上嵌入facebook帳號登入 (JavaScript SDK)](https://medium.com/@chienrongkhor/如何在網站上用facebook帳號登入-javascript-sdk-b1c0fee8aa36)
[[FB/Google] 社群帳號登入，使用Javascript SDK的Sample Code](https://dotblogs.com.tw/shadow/2018/07/05/152206)
[網頁中加入「透過Facebook登入」功能](https://icguanyu.github.io/other/facebook/)