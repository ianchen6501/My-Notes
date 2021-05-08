# HTTP (HyperText Transfer Protocol)
### 定義
是一種用於分佈式、協作式和超媒體訊息系統的應用層協定[1]。HTTP是全球資訊網的資料通信的基礎。
### HTTP 框架下的流程
瀏覽器 -> 製造 request -> Server
Server -> 製造 response -> 瀏覽器
上述的表格可以在 browser 的 devtools 看到

### request 內容
動作 / header / body
### response 內容
狀態碼 / header / body

### DNS (Domain Name Service)
一個轉換網址為實際 IP 位址的 Server
browser -> requset -> DNS -> Server

### NPM requst libray
可以用來跑 requst 的各種資訊
用法是先
> npm install request

接著到官網把 function code 複製下來後貼到新建的 index.js 檔案裡面，然後
> node index.js 

就可以看到 error / status code / body 等

[官網](https://www.npmjs.com/package/request)

### Header / Body 不是網路的那個
在每一個 request 跟 response 都有各自的 header 跟 body，header 就像紙條外面的標題，body 就是紙條的內容

### Get / Post 兩種都是 HTTP requset method
request method 大概有八種，不同的 method 就像不同的寄送方式，Get 就像明信片，把資訊都寫在外面寄送，post 是把資訊放在一個封包裏寄出
![](https://i.imgur.com/zjqlbPT.png)

### status code - response
1. 1XX - 資訊回應( hold on...)
2. 2XX - 成功回應
3. 3XX - 重定向訊息
4. 4XX - 用戶端錯誤回應
5. 5XX - 伺服器端錯誤回應

### 自製一個小 server by npm 'http'
1. 在 terminal 端利用內建的 npm 'http' library 設置一個 server
```javascript=
var http = require('http') //require http
var server = http.createServer (
    function (req, res) { //設定輸入、輸出
        console.log(req.url)
        if (req.url === '/') { //主頁面
            res.write('welcome!')
            res.end()
            return
        }
        if (req.url === '/hello') { //hello 頁面
            res.write('hello')
            res.end()
            return
        }
        if (req.url === '/redirect') {
            res.writeHead(200, {
                'lidemy' : 'good'
            })
            res.end()
            return
        }
        res.writeHead(404) //除了上述的 requst 直接出現404
        res.end()
    }
)

server.listen(5000) //port
```
2. 用 terminal 執行 server 
> node server.js
3. 在 browser 輸入下列網址
> localhost:5000/

###### tags: `week4`, `HTTP`