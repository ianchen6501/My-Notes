# NOSQL、ACID、TRANSACTION、LOCK
### NOSQL
- 非關聯式資料庫
![](https://i.imgur.com/AJQ9Mk9.png)

### TRANSACTION / ACID
- 應用在 轉帳 
- 符合 ACID 原則
- 執行完多筆指令後一次執行，避免其中部分失敗造成的異常
- transaction 要注意型態 MyISAM 不支援 TRANSACTION
- race condition
![](https://i.imgur.com/EfVoiT2.png)

### LOCK
- race condition 當伺服器處理兩個以上同時到達的 request 的時候有可能會造成"超賣"(兩個都 request success) 的情況發生，所以必須要透過 lock 來解決
- 用法在 mysql request 語句末端加上
``for update;``
- 會有效能上的損耗
- lock 有分等級
- [jmeter](https://jmeter.apache.org) 可以用來模擬 "超賣的狀況"





[ppt](https://docs.google.com/presentation/d/18dMncB442LO0MfCSjGPwjgrvGJ67I_YiVBLtqpCVnfs/edit#slide=id.p)






###### tags: `week14` `NOSQL` `ACID` `TRANSACTION` `LOCK`