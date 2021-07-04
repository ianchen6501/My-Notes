# 網站部署和 domain 設定
### 基本設定
IPV4
``
3.137.97.37
``

[phpmyadmin](http://3.131.153.195/phpmyadmin/)
```
ssh -i ~/desktop/pljim0958.pem ubuntu@3.23.197.137
```
預設主網頁位置
```
cd /var/www/html
```

### 重新開啟 關閉 apache
sudo service apache2 stop / start / restart
db(mysql) / domain / 放資料的地方

### AWS
[Getting Started with Amazon EC2](https://aws.amazon.com/ec2/getting-started/)

### DOMAIN 網域定義
- DNS: 一個伺服器將原本的IP轉換為一組網址供連結，當 clientSide 發出 request 時必須透過 DNS 獲取一組正確的 IP 位址供獲取資料。
[Domain Name（網域名稱）](http://dns-learning.twnic.net.tw/internet/intro8.html)
- domain(freenom) ``mings.gq``

### VIRTUAL HOST
conf 位址``/etc/apache2/sites-available/XXXX.conf``
[Apache – Virtual Host 設定](http://blog.faq-book.com/?p=4618)
[ubuntu 基礎架站](http://www.alvinchen.club/2018/04/12/ubuntu-基礎架站/)

### TTL - Time to live
domain 設定後可以作用的時間，以秒為單位

### ufw Uncomplicated Firewall
啟動 ufw ``sudo ufw enable``
關闢 ufw ``sudo ufw disable``

查看狀態 ``sudo ufw status`` 
查看詳細狀態 ``sudo ufw status verbose``
查看 ufw 規則及編號 ``sudo ufw status numbered``

刪除防火牆第三條規則 ``sudo ufw delete 3``

啟用 log 紀錄 ufw 連線紀錄(紀錄於 /var/log/ufw.log) ``sudo ufw logging on``

reset 防火牆 ``sudo ufw reset``

預設阻擋所有 incoming 連線 ``sudo ufw default deny incoming``
預設接受所有 outgoing 連線 ``sudo ufw default allow outgoing``

允許 ssh 連線*** ``sudo ufw allow ssh``
允許他人存取 8080 port ``sudo ufw allow 8080``
拒絕他人存取 http ``sudo ufw deny http``
拒絕他人存取 80 port ``sudo ufw deny 80``
允許他人由本機 8080 連入 ``sudo ufw allow in 8080``
拒絕本機由 8787 連線出去其他連線 ``sudo ufw deny out 8787``

允許本機 8000 到 8008 接受 TCP 封包 ``sudo ufw allow 8000:8080/tcp``
拒絕本機 9200 到 9208 接受 TCP 封包 ``sudo ufw deny 9200:9208/tcp``

允許來自203.1.1.1 的連線 ``sudo ufw allow from 203.1.1.1``
允許來自 203.0.113.0/24 的連線 ``sudo ufw allow from 203.0.113.0/24``

允許 203.1.1.1 IP 連入本機 22 port ``sudo ufw allow from 203.1.1.1 to any port 22``
允許 203.1.10/24 IP 連入本機 22 port ``sudo ufw allow from 203.1.10/24 to any port 22``

### filezilla 
- 分為 client-side / server-side
- 設定方式就是載完 filezilla 後新增連線，並選用"金鑰"的方式登入，並更改預設的連線位址為``/var/www/html``
![](https://i.imgur.com/MoEXkEY.png)

### AWS EC2 創建 instance
1. create instance
2. 建立 server 環境 - LAMP
LAMP 是一個 linux 系統的開源架站組合，L-Linux、A-Apache、M-MySQL、P-PHP

(# 部署 AWS EC2 遠端主機 + Ubuntu LAMP 環境 + phpmyadmin)[https://github.com/Lidemy/mentor-program-2nd-yuchun33/issues/15]


### 參考
[Ubuntu 18.04 LTS + Apache、MySQL、PHP (LAMP)安裝設定
](https://medium.com/@rommelhong/ubuntu-18-04-lts-apache-mysql-php-lamp-安裝設定-c46e6f54f254)
[ufw 基本指令](https://ithelp.ithome.com.tw/articles/10217802)

###### tags: `week14` `ufw` `domain`