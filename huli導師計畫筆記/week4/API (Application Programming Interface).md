# API (Application Programming Interface)
### 定義 
API 重點在於 Interface 介面這個字，是讓不同端點可以互相連接溝通，就像我們如果去到一間餐廳，就會需要跟服務生點餐，服務生會幫我們跟廚房 ORDER 餐點再送到餐桌上，API 就像服務生一樣協助我們達到目的。
"它就像是可以讓你用的一個函式庫。呼叫你想要使用的函式，並給予相對應的參數，函式便回傳給你結果，流程大概是像這樣。"
### WEB API / HTTP API
基於 HTTP 協定的 API，使用方式大致是丟出 request 然後得到 response
### 串接 HTTP API 實戰
1. 利用 Reqres.in 提供虛擬的 API 來測試 
2. 利用 request library 來發出 request 給 Reqres.in

```javascript=
const request = require('request');
request(
  'https://reqres.in/api/users/',  
  function (error, response, body) {
    console.log('body:', body); 
  }
);
```
3. 接著可以嘗試 users 後面加號碼就可以取得該號碼的資料
```javascript=
const request = require('request');
request(
  'https://reqres.in/api/users/2',  
  function (error, response, body) {
    console.log('body:', body); 
  }
);
```
![](https://i.imgur.com/gNDoPY4.png)
4. 然後可以嘗試利用 process module，process module 可以把執行過程變成 array ，只要把 process 產生的結果加到網址，就可以在 terminal 時在 node api.js 後面直接輸入號碼查詢
```javascript=
const request = require('request');
request('https://reqres.in/api/users/' + process.argv[2] ,
  function (error, response, body) {
  console.log('body:', body); 
});
```
![](https://i.imgur.com/fEPbZPK.png)
5. 另外也可以嘗試 post 一個新的資料上去，先查 [request 的資料](https://github.com/request/request#forms)看如何 post
```javascript=
const request = require('request');
request.post({url:'https://reqres.in/api/users', 
  form: {   //post的格式
    name: "morpheus", //輸入你要的資訊內容
    job: "leader"}}, 
  function (error, response, body) {
    console.log('body:', body); 
});
```
![](https://i.imgur.com/OUy2ETy.png)
6. 其他也可以自己試試看不同的 [request method](https://github.com/request/request)，如 get / head / patch /option...

###### tags: `week4`, `API`