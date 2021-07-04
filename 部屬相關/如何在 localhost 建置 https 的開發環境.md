### server 使用 express.js
### 安裝 chocolatey
chocolatey 是一個 window 環境的安裝工具，可以透過幾個指令就安裝好整個 windows 環境中你所需的軟體。
1. 用 power shell 來執行下列指令
2. ``Get-ExecutionPolicy`` check power shell 的執行權限，如果是 restricted 那就輸入 `Set-ExecutionPolicy AllSigned` 或 `Set-ExecutionPolicy Bypass -Scope Process` 來修改權限
3. 執行安裝指令 `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`

[chocolatey installization](https://docs.chocolatey.org/en-us/choco/setup)

### mkcert
> mkcert 是一個可以幫助在本地環境建立 https 協議的工具

1. 安裝 mkcert `choco install mkcert`
2. 建立 https 憑證及金鑰
`mkcert -install`
`mkcert localhost //後面接網域或ip名稱`
3. 接著 mkcer 會自動產生 localhost.pem 及 localhost-key.pem 兩個檔案

### express 建立 https 

```
var fs = require('fs'); //nodeJS 讀取和寫入檔案等的 module
var path = require('path');
var keyPath = './private.key'; //keypath
var certPath = './certificate.pem'; //certpath
var hskey = fs.readFileSync(keyPath); //讀取 keypath
var hscert = fs.readFileSync(certPath); //讀取 certpath
var express = require('express');
var https = require('https'); //引入 nodeJS https module
var app = express();
app.use(express.static(path.join(\_\_dirname, 'web')));
var server = https.createServer({ //建立 https server
	key: hskey,
    cert: hscert
}, app);
server.listen(443, function() {
    console.log('runing Web Server in ' + port + ' port...');
});
```

### reference
[Mkcert - 在 localhost 掛 HTTPS 神器](https://w3c.hexschool.com/blog/cd7b449b)
[在你的Express加上https(SSL)](https://cainmaila.github.io/2016/11/08/express-ssl/)
