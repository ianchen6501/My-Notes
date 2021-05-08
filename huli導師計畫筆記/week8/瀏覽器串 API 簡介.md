# 瀏覽器串 API 簡介
![](https://i.imgur.com/6qArbSp.jpg)
> node.js 串接 API 時，可以直接發出 req 到 server 並取得 res，但當由瀏覽器執行串接 API 的任務的時候，雖然瀏覽器也會幫我們發出 req ，但考量安全性問題，當遠端 server 回傳 res 的時候瀏覽器會確認是否有必要的 header 資訊，才會讓 local 端接收，也一併保護本地的使用者，這是由瀏覽器發出 req 的最大差異。
![](https://i.imgur.com/eYKY22u.jpg)

###### tags: `week8`
