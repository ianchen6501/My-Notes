# FETCH
### AJAX 唯二的兩種使用方式，XHR / FETCH
### 先透過 mocky 來產生 api mock
### FETCH_GET
```javascript=
fetch('url')
```
fetch 會回傳一個 promise obj，接著我們要從 promise 裡面拿 result ，要利用到 ``.then()``
```javascript=
fetch('url').then(a => {
console.log(a) //callbac function
})
```
但拿到資料後如果要取得裡面 body 的內容，要透過 ``.text()`` ，弔詭的是透過這樣的方式會再拿到一個 promise(中獎了)，所以要透過 ``.then`` 的方式再提取一次
```javascript=
fetch('url').then(a => {
  a.text().then(res => {
  console.log(res) //要用 cb function 拿回來
  })
})
```
另外再說一個結論 .then 裡面如果有 return 一個值的話，可以再下一個 .then 的 cb function 去取得那個值
```javascript=
  fetch('url')
  .then(response => {
    return response.json()
  }).then(abc => {
    console.log(abc)
  })
```
### fetch 錯誤定義
ㄧ般的 htmlcode 500 等不算是錯誤，因為瀏覽器有確實接收到 response 只有那種沒有 response (網址錯誤等)才算是 fetch error

### 錯誤處理
ㄧ般在同步的程式碼(與 web 無關)可以用 ``try( ) catch()``來處理，但在非同步的程式裡邊則不行，所以要改用 ``.catch`` 的方式來處理
```javascript=
  // error handle
  fetch(api_500)
  .then(response => {
    return response.json()
  }).then(json => {
    console.log(json)
    //do something
  }).catch(err => { 
    console.log("error:", err)
  })
```

### fetch_POST
```javascript=
  fetch(api_200, {
    method: "POST",
    body: JSON.stringify(data), // 以 json 來傳輸，要搭配 content-type 一起修正
    headers: new Headers({
      'Content-Type': 'application/json'
    })
  }).then(res => res.json())
    .catch(error => console.error('Error:', error))
    .then(response => console.log('Success:', response));
```

### fetch_credential
fetch 預設是不帶 cookies 的，所以如果要帶 cookie 要在 post 裡面加上``credentials: 'include',``

### mode : 'no-cors'
因為 cors 的 same-original 策略，所以就算設定了 ``mode : 'no-cors'`` 也只是告訴 browser 說"我知道會拿不到資料，那你就回傳空的資料給我就好"

### promise
是一種 obj 裡面可以設定兩種狀況的回傳值(resolve / reject)
```javascript=
const myPromise = new Promise((resolve, reject) => {
resolve()
reject()
}
```

### async / await

### .finally(()=> {})
[Promise.prototype.finally()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise/finally)



### *setTimeout 失效檢討
``setTimeout(function(a), milesec)``如果函式有帶參數就會造成時間延遲失效，解決的方式可以靠匿名函式解決
```javascript=
setTimeout(() => {
//do something
}, ms)
```
### *new 
new 會創建一個新的物件，而沒有 new 的狀況會指向原本的物件，所以用下面的例子來看，no new 會指向原本的 ``person('lee')``，而 withnew 則是一個 new obj
```javascript=
function person(_name){
	this.name = _name;	
	this.getname = function () {
		return "hello " + this.name;
	}	
	return this;
}
var noNew = person("ace");
var withNew = new person("ace");

var p = person("lee");
console.log(p === noNew); //true
console.log(p === withNew); //false

console.log(noNew.getname()); // hello lee
console.log(withNew.getname()); //hello ace
```

### 非同步(Asynchronous)與同步(Synchronous)


###### tags: `week13` `fetch`