### 基礎語法:
``req.params._`` 拿到 querystring
``req.body._`` 拿到 post 內
``req.query`` get querystring
[NodeJS-Express](https://kanboo.github.io/2017/12/27/NodeJS-Express/)

---
### template engine
- template engine ``Pug`` ``Mustache`` ``EJS``
- install ``npm install ejs --save``
- set engine (index.js) ``app.set('view engine', 'ejs')``
- create a new folder ``mkdir views``	
- put ejs file in it ``mv index.ejs views``
- create a route to render index.js 
```js
app.get('/', function (req, res) {
  res.render('index', { title: 'Hey', message: 'Hello there!' })
})
```
[EJS 官網](https://ejs.bootcss.com)

---
### mysql
- ``npm install mysqljs/mysql``
```js
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});

connection.connect();

connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});

connection.end();
```

---
### middleware 中介層

---
### body parsor
express 僅提供提取 get 的方法，但針對 JSON、RAW body、Text body、Url-encoded form body 需要依靠額外的 middleware 就是 body parsor
[expressjs - body-parser](https://github.com/expressjs/body-parser)
- ``npm install body-parser``
- ``var bodyParser = require('body-parser')``
- ``app.use(bodyParser.json())``
- ``app.use(bodyParser.urlencoded({ extended: false }))``
---
### express-session
``npm install express-session``
```js
//引入 express-session
var session = require('express-session')
//設定 session option
app.use(session({
  secret: 'keyboard cat', //加密方式
  resave: false, //強制將 session 存回 session store
  saveUninitialized: true, //強制將未初始化的session存回 session stor
  cookie: { secure: true }, //設定sessionID 的cookie相關選項，預設{ path: ‘/’, httpOnly: true, secure: false, maxAge: null
  }
}))
//設定 session
req.session.sessionname = value
//重新產生 session
req.session.regenerate(function(err) {
  // will have a new session here
})
//清除 session
req.session.reload(function(err) {
  // session updated
})
//重新載入 session
req.session.reload(function(err) {
  // session updated
})
```


```



[express-session](https://github.com/expressjs/session)
[express-session-document](https://expressjs.com/en/resources/middleware/session.html)

---
### connect-flash
用來顯示錯誤訊息或成功訊息，可以在驗證登入或輸入的地方加入錯誤處理，並把 errorMessage 回傳到 view 裡面，當作錯誤訊息。
- ``npm install connect-flash``
```js
const flash = require("connect-flash")
app.use(flash())
//寫入 flash
req.flash('info', 'flash is back!') //在 info key 裡面存入 'flash is back!'
//讀取 flash
req.flash('info')
```

---
### bycrypt - hash
hash module
[node.bcrypt.js](https://github.com/kelektiv/node.bcrypt.js)

### 資安相關
如果我們今天是用 <%= %>，express - template engine 自動會針對 XSS 處理 escape，除非我們改成 <%- %> 那就會解除 escape 的功能

### cors
如果沒有開啟 cors ，就會用預設的 same-origin-polocy
