### CSR vs SSR
CSR 一開始只會有一個錨點，如 react 裡面的 root div，當打包專案的 bundle.js 下載完成後，在依據 router 由 JavaScript 去拿資料來組成畫面。

SSR 則是沒有那個錨點 HTML ，第一次的畫面是由 server 傳過來的，server 會根據 URL path 來決定 render 的內容並回傳給 browser 來 render

**所以在 SPA 中 SSR 和 CSR 的不同就只有在第一次的畫面是由誰 Render 而已**

### SSR的優缺點
#### 優點
1. 有利於 SEO
2. 使用者看到畫面的時間會比較早，效能也比較好
#### 缺點
1. 學習門檻高，需要學習 server
2. 第一次 render 是在 server 上，如果有 ``window`` 指令會造成錯誤

