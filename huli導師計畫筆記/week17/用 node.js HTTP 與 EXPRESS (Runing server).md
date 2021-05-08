# 用 node.js HTTP 與 EXPRESS (Runing server)

---
## 建立基本的連線
我們可以利用 node.js 內建的 http 模組來讓 node.js run 一個簡易的 server
(這邊預設是由本機連入)
```javascript=
const http = require('http') //引入 node.js 原生模組 http

const server = http.createServer(handler) //建立 server ，這邊也可以直接把 function handler 引入

function handler(req, res) {
  console.log(req.url)
  res.write('hello')
  res.end() //結束 res
}

server.listen(5001) //建立 port 監聽
```
- req 回傳的內容也可以是 html tag
- 透過設定條件來讓不同的 url 有不同的回應
```javascript=
function handler(req, res) {
  console.log(req.url)
  if (req.url === "/hello") { //url: /hello
    res.write('hello')
  } else if (req.url === "/bye") { //url: /bye
    res.write('<h1>bye</h1>') //html tag
  } else {
    res.write('invalid url')
  }
  res.end()
```
- 透過 ``.writeHead()`` 來設定 <font color = #ba55d3>http code</font> 及 Content-type

[其他說明請參考](https://nodejs.org/zh-cn/docs/guides/anatomy-of-an-http-transaction/)

--- 
## 改成用 EXPRESS 來建立基本連線
1. ``npm init -y`` 建立 node 環境
2. ``npm install express --sava`` 安裝 EXPRESS
3. ``touch index.js`` 建立 server 
```javascript=
const express = require('express')
const app = express()
const port = 5001 //這邊注意不要用常見的 80 或 ftp

app.get('/', (req, res) => { //也可以改用 post / delete 等 http method
  res.send('hello')
})

app.get('/hello', (req, res) => {
  res.send('hello man')
})

app.get('/bye', (req, res) => {
  res.send('yo bye')
})

app.listen(port, () => { //監聽 port
  console.log(`Example app listening at http://localhost:${port}`)
})
```
# APACHE + PHP vs EXPRESS
### APACHE + PHP
- 瀏覽器 req 會先由 APACHE 接收後再交由 PHP 去跟資料庫溝通，最後再由 APACHE 接收資料

<img width=70% height=70% src='https://i.imgur.com/KmZusul.png'></img>
### EXPRESS
- EXPRESS 可以省略 PHP 作業，直接整合在一起
- 好處是不會受到資料夾路徑的限制，可以改變 url

<img width=70% height=70% src='https://i.imgur.com/Kln6oOy.png'></img>



###### tags: `week17` `HTTP` `EXPRESS`