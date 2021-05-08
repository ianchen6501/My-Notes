# 留言板修正 - 密碼 hash
### 雜湊 hash
當一組密碼經過 hash 後會產生一個對應的結果，hash 針對無線種可能的密碼組合是一個多對一的狀況，有點像餘數，1、1000、1999經過 %999 的處力都會得到一樣的數值。
因此資料庫的修正方式其實是對輸入的密碼進行 hash 後存入，下一次使用者再輸入密碼時，只要比對雜湊結果一致就可以。

[md5](https://www.md5hashgenerator.com) 已被驗證有破解
[sha256](https://emn178.github.io/online-tools/sha256.html)

因此我們再驗證密碼時，其實可以用 ``password_hash(var, PASSWORD_DEFAULT)``這個函數來幫密碼 hash。驗證時可以用 ``password_verify()``這個函數來比對是否一致。

###### tags: `week11`