# 認識 this
### 物件導向
在物件導向的環境中，this 會指涉到該物件。
```javascript=
class flower {
  constructor(name) {
  this.name = name
  }
  sayHello () {
  console.log('this.name')
  }
}

var sun_flower = new flower('sun_flower')
sun_flower.sayHello() //sun_flower
```

### 在非物件導向的部分 - node、瀏覽器
在非物件導向的部分，this 會指向全域 global ，所以 global 是 node 或瀏覽器會回傳不同的資訊
```javascript=
function test() {  
	function inner() {
		console.log(this)
	}
	inner()
}
test()
```
但假設我們今天開啟"嚴格模式"，this 就會出現 undefined
```javascript=
'use strict';
function test() {  
	function inner() {
		console.log(this)
	}
	inner()
}
test() //undefined
```

### 來談談 call、apply
call 和 apply 其實很相像，都會回傳一個函式運算的結果，我們先來看看兩個的語法，
1. call : ``fun.call(thisArg[, arg1[, arg2[, ...]]])``
2. apply : ``fun.apply(thisArg, [argsArray])``

可以看到兩個傳入的第一個參數都是 this 的值，差別在於後面的參數一個是傳入以 , 分開的不同參數，另一個則是陣列。
```javascript=
'use strict';
function test(a, b, c) {
	console.log(a ,b ,c)
	console.log(this)
}
test.call(123, 1, 2, 3) //1 2 3 123
test.apply(123, [1, 2, 3]) //1 2 3 123
```

### 有關於 this 的呼叫方式
如果我們今天創建了一個 obj 的物件，並在裡面放入一個 function ``console.log(this)``，用 ``obj.function()`` 和 ㄧ般 call function 得到的結果會一樣嗎? 答案是不一樣，因為前者有把 this 帶入。
在物件裡面 call this ，預設規則會回傳 function 前面的那一個東西。
```javascript=
'use strict';

const obj = {
	a:123,
	inner: {
		test: function() {
			console.log(this) //obj
		}
	}
}

obj.inner.test() //oop 的呼叫型式
obj.inner.test.call(obj.inner) //this -> obj.inner

//換一種呼叫方式，會得到不同結果
var func = obj.inner.test
func() //undefined
func.call(undefined)
/* 所以我們可以得到以下結論
1. 跟 OOP 無關的環境 -> this === window / undefined
2. OOP -> this === instance
3. 如上述用物件內容的方式 call this -> this === 傳進的參數
*/
```
### this 在 DOM 監聽裡面的回傳值
會回傳正在執行的物件
```javascript=
document.querySelector('div').addEventListener('click', () => {
  consol.log(this) //'div'
})
```

### bind
上面提到的狀況，不同的呼叫 this 的方式會得到不同的結果，那假若我們用一般的方式 ``var variable = obj.thisfunc`` 呼叫 this 又想綁定一個數值給他，可以用 ``bind()`` 的方式綁定一個數值，注意的是之後 variable 的 this 值就不能再改變了。
```javascript=
'use strict'
//先來個小練習喔~~
function log() {
  console.log(this);
}

var a = { a: 1, log: log };
var b = { a: 2, log: log };

log(); //window, strick -> undefined
a.log(); //{a:1, log: log}
b.log.apply(a) //{a:1, log: log}


//接著我們回顧一下 this 的不同 call 法會回傳什麼東西
const obj = {
  num: 1,
  test : function() {
    console.log(this)
  }
}


obj.test() // obj
const c = obj.test
c() //undefined

//如果今天想要有一個函式可以綁定 obj 跟 obj.test ，我們可以用 bind()
const d = obj.test.bind(obj)
d() //obj

//但假如今天已經用 bind 綁定 this 的話，後面就算用 call 也無法更改了
d.call('123') //obj
```
### this 在 arrow function 裡面的回傳值
用 arrow function 跟在一般 function 裡面 call this 會有不一樣的行為(可以當作一個特例)，在 arrow function 裡面會回傳 this 原本建立時的回傳值，而不是像一般 function 會回傳 global 或 undefined
```javascript=
class test {
  run() {
    console.log('run this:', this)
    setTimeout(() => {
      console.log(this)
    },180)
  }
}

const t = new test()
t.run() //run this: test {}, test{}
```








###### tags: `week16` `物件導向` `OOP` `this`