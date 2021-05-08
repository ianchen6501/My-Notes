# API 工具 - CURL 、 相關指令
### CURL 安裝步驟
先至 [curl](https://curl.haxx.se) 下載封包，之後 terminal 就會有 curl 工具
### CURL 基本指令
- curl 發出 get 並取得 response
```javascript=
curl 'http://...'
```
- curl -i + 網址 : 可取得 status code 等額外資訊
```javascript=
curl -i 'http://...'
```
- 利用導向方式，儲存網頁
```javascript=
curl 'http://...' > file name
```
- 只取得 header
```javascript=
curl -I 'http://....'
```

### 好用指令
- nslookup + 網址
- ping + 網址 : 可以測試能不能連到
![](https://i.imgur.com/iA2U80K.png)
- telnet + address : 測試 port (PTT) 能不能連到
```javascript=
telnet + address + port number
```

###### tags: `week4`