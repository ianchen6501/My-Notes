# php 與 Apache 原理
### 實際網路執行流程
request => apache(server) => php => output => apache => response

apache
function response(request) {
    response = php(request)
    send response
}

### 網址與檔案路徑關係
- apache 預設是用檔案路徑當作網址，但其實可以更改路徑，更改的方式是找到 /XAMPP/apache/conf/httpd.conf 檔裡面就可以設定如 documentroot / serveroot / servename 等值
- 但像 facebook 等一般網站我們看到的網址都不會是...pht 等結尾的原因是，那些網站有另外設定一個方式讓網址可以存取到不同名稱的檔案。








###### tags: `week9` `apache` `php`