因為幫朋友做了靜態網站，把網站架構完成後終於要進入部屬的部分了，因為之前部屬大部分都忘光了 XD，所以重新用這篇作紀錄。

### 架構

因為是靜態網站，只包含，打算把網頁內容部屬在 aws ec2 上面，然後再利用 gandi 的 domain 進行轉址。
另外再 aws ec2 上面會另外安裝 nginx 進行 proxy 反向代理。

### DNS 紀錄分類

#### 紀錄範例

`www 10800 IN A 123.123.123.123 //子網域+TTL+紀錄形式+IP`

#### A 紀錄

- 適合用在 IPv4 的靜態 IP

#### AAAA 紀錄

- 適合用在 IPv6 的靜態 IP

#### CNAME 紀錄

-
