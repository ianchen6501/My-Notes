# 網站部屬(huli 詳解)
## AWS EC2 申請
- 主機位置
會影響連線速度(越近越快)和價錢(美東/美西較便宜)。
- choose a Amazon Machine Image(映像檔)
像是用哪一個映像檔安裝，本次選擇 ubuntu 18.04
- choose an instance type 
選擇主機
- Configure instance Details
一些網路設定，可以先用預設
- Add Storage
- Add tags
方便管理主機
- Configure Security Group
設定連線方式 (SSH / Http)，Source 預設 0.0.0.0/0 表示所有 IP 都可
- create a private key
下載一個 key pair 檔案

## terminal 操作
``top`` 可以看到主機的狀態(q 離開)
``sudo apt upgrade && sudo apt dist-upgrade``
更新 ubuntu
``sudo apt install taskel`` 安裝 taskel
``sudo taskel install lamp-server`` 安裝 lamp
``curl http://localhost``連接 localhost (測試 myphpadmin)
``telnet IP 80``連接 ip (測試用)
``pin IP `` 連接 ip (測試用)

## 資料庫設定
``sudo apt install phpmyadmin``安裝 phpmyadmin(apache2)
``root / password``phpmyadmin 預設帳密
``sudo mysql -u root mysql``指令登入 mysql
``flush privilege``接著設定 mysql 密碼
``mysql -u root -p`` 登入mysql
- 要確保遠端也可以連線 mysql
1. 確認防火牆有開 mysql (3306)
2. 確認 mysql 使用者有開任意主機連線
- 為何在上述條件未達成的狀況底下,phpmyadmin 可以連線 mysql 是因為對 mysql 而言 phpmyadmin 是 localhost(存在同一台主機上)

## php 設定
``IP`` 直接在瀏覽器輸入 IP 會連到 /var/www/html 裡面的 index.php
``sudo chown ubuntu /var/www/html``
chown -> 'change ownership' : 更改 /var/www/html 為 ubuntu 用戶也可以有權限
``ls -al`` 列出所有檔案

### mysql 匯出並匯入 遠端 mysql
在要匯出的 database 點 export 並選擇要匯出的 table，並在要匯入的 database 點匯入
注意如果出現``ERROR 1273 (HY000): Unknown collation: 'utf8mb4_0900_ai_ci'``的錯誤，解決方式是打開匯出的 .sql 檔案找到 utf8mb4_0900_ai_ci 把他替換成 utf8 並重新匯入
[Linux中MySQL表的导出导入指令以及导入失败ERROR 1273 (HY000): Unknown collation: 'utf8mb4_0900_ai_ci'解决方案](https://www.jianshu.com/p/788dceb93eff)

### php 修正
``/etc/php/7.4/apache2/php.ini``預設的 php 設定檔位置
找到 php.ini 裡面的 short_open_tag 改成 on 就可以使用 <? ?> 的短 php 標籤語法









###### tags: `week14`