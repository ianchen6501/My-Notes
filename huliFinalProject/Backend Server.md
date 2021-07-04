### phpmyadmin
username : root
password : hittheroad
phpmyadmin url : http://172.31.26.153/phpmyadmin/index.php
ssh -i ~/desktop/hittheroad.pem ubuntu@172.31.26.153

### 遠端連線確認事項
1. 新建資料庫，這邊以 aws server 為主
2. 安裝 lamp、phpmyadmin(資料庫才可以 run 起來)
3. 確認 mysql : 3306 port ，所以要確認 ubuntu 防火牆和 ec2 instance 都沒有檔 3306 port

*進入 mysql 作業``sudo mysql -u root mysql``

### 遠端部屬
``sudo apt install nodejs`` 在 ubuntu 安裝 node
`sudo apt install npm` 在 ubuntu 安裝 npm
`git init` `git remote add url url` `git pull origin master` 抓取 backend source code
`npm init` deploy npm
`npm install` download npm 

### 架構
資料庫 : aws EC2 + phpmyadmin
server : express + nginx / pm2
client : react

### DB-phpmydamin
migration 

### express
獨立 server ，可以不用根據檔案結構只根據路由就回傳相關資訊
會分成 MVC 三個部分，models 寫要跟資料庫拿資料的 function(透過 mysql)，controlers 則是負責接受 client request(react)

### express-session
可以讀寫 session，可用來做驗證

[](https://blog.huli.tw/2019/08/09/session-and-cookie-part3/)

### connect-flash
只會顯示一次，有點類似 session 但會在 reload 後消失
使用:
``app.use(flash)``
``req.flash('errormessage')``
``res.render()``

### sequelize
自動產生 models 的資料結構
在 config.js 設定連線
連線資料庫只要 require model ``const db = require('/models')``	

### linux 權限
linux drwxr-xr-x 
第一位表示文件类型。d是目录文件，l是链接文件，-是普通文件，p是管道
第2-4位表示这个文件的属主拥有的权限，r是读，w是写，x是执行。
第5-7位表示和这个文件属主所在同一个组的用户所具有的权限。
第8-10位表示其他用户所具有的权限。
``ls -ld /var/www/folder`` 檢查資料夾權限
``chmod 777 /var/www/folder`` 開啟該資料夾針對使用者 wrx 權限
``sudo chown -R ubuntu:ubuntu /var/www/html`` 開啟 ubuntu 權限

### JWT (json web token)


### SSL 憑證
#### 利用 ssl for free
申請 [SSL 憑證](https://manage.sslforfree.com/dashboard)，並下載憑證檔案
部屬到 ubuntu :
- 把 Certificate 放到指定資料夾
1. certificate.crt & ca\_bundle.crt : /etc/ssl/
2. private.key : /etc/ssl/private/
3. budle
- 調整 apache 設定檔	
位址: /etc/apache2/sites-enabled/your\_site\_name
或執行 ``sudo a2ensite your\_site\_name``
在裡面要設定一個 vertual host (或考慮用 nginx)，這邊要記得先備份 .conf 檔
```js
server {
  **listen443;
    ssl on;
    ssl\_certificate /etc/ssl/your\_domain\_name.pem;** _(or  bundle.crt)_
  **ssl\_certificate\_key /etc/ssl/your\_domain\_name.key;**
    server\_name your.domain.com;
    access\_log /var/log/nginx/nginx.vhost.access.log;
    error\_log /var/log/nginx/nginx.vhost.error.log;
    location / {
    root  /home/www/public\_html/your.domain.com/public/;
    index  index.html;
    }
    }
```
3. 修改 certificate 檔名稱
-   **SSLCertificateFile**: (certificate.crt)
-   **SSLCertificateChainFile**: (ca\_bundle.crt)
-   **SSLCertificateKeyFile**: (private.key)

4. 測試 config 檔
``sudo a2enmod ssl`` 啟用 apache ssl
``apachectl configtest``
5. 重啟 apache
``apachectl stop``
``apachectl start`

#### 利用 cloudflare
- 原理
透過在網路傳輸路徑中加上一個 cloudflare 的 DNS server ，建立 client 與 cloudflare 中間的 SSL 連線(可選擇 full / flexible 等模式)。
![](https://miro.medium.com/max/900/1*LAz5GAXSWgjZI0DJhyToCA.png)
- 流程
- 在 [cloudflare]() 註冊並新增一個 domain 為 https 連線
- 在原本的 DNS 服務商更改 nameServer 為 cloud flare 的 name Server
- 名稱伺服器(gandi)
1. `christina.ns.cloudflare.com`
2. `ian.ns.cloudflare.com`

#### refer
[[AWS] 透過 FileZilla 使用 key-pairs 登入 AWS EC2 存取檔案](http://www.jysblog.com/coding/web/aws-透過-filezilla-使用-key-pairs-登入-aws-ec2-存取檔案/)
[調整 ubuntu 存取權限](https://www.edureka.co/community/2722/amazon-aws-filezilla-transfer-says-permission-denied)

[SSL (Secure Sockets Layer) 通訊安全協定](SSL%20(Secure%20Sockets%20Layer)%20通訊安全協定.md)
[https 簡介](https%20簡介.md)