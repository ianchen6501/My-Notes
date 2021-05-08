### ㄧ般網路的情況
![](Pasted%20image%2020201019144219.png)

### proxy server 代理伺服器
代理伺服器主要指的是代理 client-side，具有下列功效
1.  具有隱私，可以隱藏真實 id
2.  可以儲存 cache ，可以預先儲存 response ，有助於緩解大量流量
3.  有時也可能成為釣魚網站的掩護
![](Pasted%20image%2020201019143854.png)

### reverse proxy 反向代理
反向代理其實就是代理 server-slide ，好處是原本 80 port(http) 只能架一台 server 提供一個服務，但透過反向代理就可以同時架好幾個服務，並透過一個代理伺服器來連接。
![](Pasted%20image%2020201019143633.png)
![](Pasted%20image%2020201019145003.png)

### Nginx
提供反向代理的服務，假設我們要在 1.1.1.1 ip 同時設置 imgur / tinyurl 服務，nginx 可以判斷從不同 domain 來的 request 並轉給相對應的 server
![](Pasted%20image%2020201019145247.png)

### nginx setup
> nginx 的原理就在於先關掉 apache server，並另外透過 nginx server 來執行 reverse proxy
1.  ``ssh -i ~/desktop/pljim0958.pem ubuntu@3.137.97.37`` link ubuntu
2.  ``sudo apt install nginx`` 、 ``sudo apt update`` install nginx
	1.  ``sudo /etc/init.d/apache2 stop`` close apache
3.  ``sudo ufw app list`` 、 ``sudo ufw allow 'Nginx HTTP'`` check and open fire walls
4.  ``systemctl status nginx`` check nginx status
5.  ``sudo systemctl start nginx`` start web server 
``sudo systemctl stop nginx`` 
``sudo systemctl restart nginx`` 
``sudo systemctl reload nginx`` 改 conf 可以直接 reload
7. nginx 建立完成接著進行網站建置，在 ubuntu 建立 npm 環境 ``sudo apt install -y nodejs``，並另外安裝 express 、 pm2等，要建立 profile 修改 node root 權限參考[這邊](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally)
8. 接著用 pm2 把網站跑起來
9. 進入 ``/etc/nginx/sites-available`` 新增要轉址 server 的 conf 檔，格式如下
```js
server {
        listen 80;

        root /var/www/example.com/html;
        index index.html index.htm index.nginx-debian.html;

        server_name example.com www.example.com;

        location / {
                try_files $uri $uri/ =404;
        }
}
```
```js
server {
        listen 443;
        server_name example.com www.example.com;	
        location / {
        	proxy_pass http://3.23.193.137:5003;
        }
}
```
10. 建立 conf 連結 ``sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/``，原因是為了後續管理方便，檔案的編修建立在 sites-avalable 裡面，並利用 symbolic link 的方式來建立連結，避免直接在 sites-enabled 裡面編修檔案


### 常用指令
``apt install net-tools`` 安裝 net-tools
``ssh -i ~/desktop/pljim0958.pem ubuntu@3.137.97.37``登入ubuntu
``ps ax | grep firefox`` 找出 PID
``sudo netstat -tulpn | grep LISTEN`` 查看 port 狀態
``sudo systemctl start apache2``
``sudo systemctl status apache2``
``cp nginx.conf nginx.conf.bak`` back up conf

### reference
[how to install nginx on ubuntu](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04)