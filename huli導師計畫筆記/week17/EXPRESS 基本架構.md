# EXPRESS 基本架構
### MVC
<img width=70% height=70% src="https://i.imgur.com/m1jprVC.png"/>

### Using template engines (View)
- 一個可以自動渲染建立 html 模板的 module
- 這邊我們使用 ejs ``npm install ejs --save``
- 接著在 index.js 選擇 render engine ，並設定 get res
```javascript=
app.set('view engine', 'ejs') //設定 view enging

//用 template engine 來 render
app.get('/pug', function (req, res) { 
  res.render('index', { title: 'Hey', message: 'Hello there!' }) //可以直接寫檔名，不用寫附檔名系統會自己判斷
```

### 建立一個基本的 todos
1. 首先在 index.js 建立 todos array，並建立一個 get render，把 todos 傳過去 render
```javascript=
//建立一個簡單可以看的 todolist
const todos = [
'firstTodo', 'secondTodo', 'thirdTodo' 
]
app.get('/todos', (req, res) => {
res.render('todos', {
  todos: todos //ES6 如果 key = value 可以直接寫成 "todos" 省略分號後面的東西
})
```
2. 接著建立一個 todos.ejs，裡面用類似 php 的結構把 todos 帶進來並顯示
```javascript=
<h2>todos</h2>
<ul>
  <% for (const todo of todos) { %> //用 <% %> 裡面就可以執行 javaScript
    <li><%= todo %></li> //加 "=" 代表後面的東西要輸出 
  <% } %>
</ul>
```
![](https://i.imgur.com/LXjQxJ7.png)
3. 接著我們可以建立一個 todo 的分項顯示頁面，藉由在 url 後面加上 id 的方式，首先先建立一個新的 get res 
```javascript=
  app.get('/todos/:id', (req, res) => {
    const id = req.params.id //拿到 url 裡面的 id
    res.render('todo', {
      todo: todos[id]
    })
  })
```
4. 另外建立一個新的 todo.ejs
![](https://i.imgur.com/SCWk0Em.png)

5. 接著我們來重構目前的簡易留言板，做出 model 跟 controler，所以先建立兩個資料夾，裡面放 js 檔案。
#### <font color=#11111>model 放資料供取用</font>
```javascript=
//資料
const todos = [
  'firstTodo', 'secondTodo', 'thirdTodo' 
]
//建立不同拿取資料的方法
const todoModel = {
  getAll: (req, res) => {
    return todos
  },
  getId: id => {
    return todos[id]
  }
}
//export 資料
module.exports = todoModel
```
#### <font color=#11111>control 則是提供各種功能，供 index.js 串接</font>
```javascript=
//資料
const todoModel = require('../models/todo')
//建立不同拿取資料的方法
const todoControler = {
  getAll: (req, res) => {
    const todos = todoModel.getAll()
    res.render('todos', {
    todos //ES6 如果 key = value 可以直接寫成 "todos" 省略分號後面的東西
    })
  },
  getId: (req, res) => {
    const id = req.params.id //拿到 url 裡面的 id
    const todo = todoModel.getId(id)
    res.render('todo', {
      todo
    })
  }
}
//export 資料
module.exports = todoControler
```
6. 所以原本的 index.js 就可以重構如下
```javascript=
app.get('/todos', todoControler.getAll)
app.get('/todos/:id', todoControler.getId)
```





[EXPRESS - Using template engines](https://expressjs.com/en/guide/using-template-engines.html)







###### tags: `week17` `EXPRESS` `MVC`