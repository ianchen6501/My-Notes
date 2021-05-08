	### 遠端連線伺服器
透過諸如 telnet / rsh / ssh 等方式登入遠端的 server linux 系統進行操作，可以同時讓多人遠端利用伺服器進行運算。
telnet / rsh 等已經等因為是明碼傳輸，目前已經比較少人使用
ssh 則是密碼傳輸(非對稱加密)

### 遠端連線方式
`ssh \[-f\] \[-o 參數項目\] \[-p 非正規埠口\] \[帳號@\]IP \[指令\]`
選項與參數：
-f ：需要配合後面的 \[指令\] ，不登入遠端主機直接發送一個指令過去而已；
-o 參數項目：主要的參數項目有：
	ConnectTimeout=秒數 ：連線等待的秒數，減少等待的時間
	StrictHostKeyChecking=\[yes|no|ask\]：預設是 ask，若要讓 public key
           主動加入 known\_hosts ，則可以設定為 no 即可。
-p ：如果你的 sshd 服務啟動在非正規的埠口 (22)，需使用此項目；
\[指令\] ：不登入遠端主機，直接發送指令過去。但與 -f 意義不太相同。

### 連線錯誤修正方式
![](Pasted%20image%2020210413071424.png)
遇到上面的問題可以嘗試編修 `root/.ssh/knownhosts` 把既有連線刪掉重新登入

## Linux
### 基本概念
- 每個檔案都會包含 user / group / other group 三種不同開放的權限，我們可以設定對這三種身分開放何種權限。
- root 可以進行所有的編修。
- 使用者身分記錄在 `/etc/passwd`
- 密碼記錄在 `/etc/shadow`
- 群組記錄在 `/etc/group`

### Linux basic command
`id` 查看登入的 uid、gid 等


### ssh 連線整理
final-project_hit-the-road
`ssh -i ~/desktop/pljim0958.pem ubuntu@3.23.193.137`



### reference 
[鳥哥的私房菜](http://linux.vbird.org/linux_server/0310telnetssh.php#remote_access)