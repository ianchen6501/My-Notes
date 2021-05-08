# 資料格式 - XML / JSON
### 資料在傳輸時必須定義格式，可以自訂格式或常見的 XML, JSON
### 純文字及自定義格式
在使用純文字或自定義格式時，需在 request 端額外處裡
```javascript=
if (response.body.indexOF("狀態 : 良好") >= 0){
  ...
}
```
### XML (Extensive Markup Language)
類似 HTML ，都是 Markup 標記格式，例如
```xml=
<user>
<id> morpheus </id>
<job> leader  </job>
<createdAt> 2020-07-11T00:57:05.632Z </createdAt>
</user>
```
### JSON
[JSON](https://developer.mozilla.org/zh-TW/docs/Learn/JavaScript/Objects/JSON) 是依照 JavaScript 物件語法的資料格式，JSON 可能是物件或字串。當你想從 JSON中讀取資料時，JSON可作為物件；當要跨網路傳送 JSON 時，就會是字串。

舉例來說， reqres.in 回傳的格式就是 JSON 所以其實我們可以讀取其內容
```javascript=
const request = require('request');
request ('https://reqres.in/api/users/2', 
  function (error, response, body) {
    const json = JSON.parse(body) //JSON.parse 會把一個JSON字串轉換成JavaScript的數值或是物件，因此要傳入一個 JSON 格式的 arr
    console.log(json.data); 
});
```
![](https://i.imgur.com/TBMOjKs.png)

相對的我們也可以反過來操作，創建一個 obj 然後轉換為 JSON 格式
```javascript=
const obj ={
    name : 'ian'
}
console.log(JSON.stringify(obj)) 
//JSON.stringify : 把 JavaScript 物件轉為 JSON
```
![](https://i.imgur.com/WmIuWM1.png)

### 小觀念:所有的資料格式都可以在所有的程式語言中使用，只要找到適當的 parser

###### tags: `week4`, `XML` `JSON`