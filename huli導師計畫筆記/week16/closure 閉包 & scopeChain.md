# closure 閉包 & scopeChain
### 常見的 closure 現象
以下面的例子來說，test() 執行完後，他的 VO 會消失，裡面的資料也會不見，但奇怪的是 inner 卻把 a 的值給存了起來...
```javascript=
function test() {
  var a = 10
  function inner() {
    a++
    console.log(a)
  }
  return inner
}

var func = test()
func() //11
func() //12
func() //13
func() //14
```
也可以另外看一個應用的例子，這邊我們利用 closure 的特性，來幫助記住已計算的結果，避免每次系統都要重新計算
```javascript=
//基本應用 cache
function complex(num) {
  //複雜計算
  console.log('calculate')
  return num * num * num
}
//cache -> 簡化每一次的計算過程，把計算結果儲存起來
function cache(func) {
  var ans = {} //透過 ans 把值記住
  function inner(num) {
    if(ans[num]) {
      return ans[num]
    }
      return ans[num] = func(num) //var ans[20] = complex[20]
  }
  return inner
}

var cacheComplex = cache(complex)
console.log(complex(30))
console.log(complex(30))

console.log(cacheComplex(30))
console.log(cacheComplex(30))
```

### 定義
- 在一個 function 裡面 return 一個 function ，被 return 的 function 就會帶有全域 VO / AO 的資料，像上面的那個例子， a 的值就被 lock 在 inner 裡邊
- 會達成上述的現象，其實要回去再了解 ECMAscript 裡面提到的 scope 及 scope chain

### scope / scope chain
- 前面我們有提到每執行一個 function 之前，會先建立 EC(execution context) 以及 VO(variable object)，那在 ECMAscript3 裡面有提到每一個 EC 其實都會伴隨一個 scope chain 物件，
> Every execution context has associated with it a scope chain. A scope chain is a list of objects that are searched
when evaluating an Identifier. When control enters an execution context, a scope chain is created and populated
with an initial set of objects, depending on the type of code.
- 那我們再來看 scope chain 是怎麼樣的一個東西，從敘述我們可以知道 ``scopechain = AO + [[scope]]``
> The scope chain is initialised to contain the activation object followed by the objects in the scope chain stored in
the [[Scope]] property of the Function object.
- 那 AO(Activation Object) 又是什麼呢?我們其實可以把它看成執行的 function EC 的 VO
> When control enters an execution context for function code, an object called the activation object is created and
associated with the execution context. The activation object is initialised with a property with name arguments and
attributes { DontDelete }. The initial value of this property is the arguments object described below.
The activation object is then used as the variable object for the purposes of variable instantiation. 
- 所以我們其實可以把上述的現象，用下面的 code 來表達，
```javascript=
global EC: {
  VO: {
  }
}

function EC: {
  AO: {
  }
  scope chain: [function EC.AO, [[scope]]]
}

enter function EC =>
Scope Chain: [AO, [[scope]]]
```
- 那我們再來用一個例子來解釋 scopeChain 是怎麼作用的，可以看到因為 scopeChain 把整個作用域的關係給串起來，當本層的 AO 找不到時，就會往上找
```javascript=
var a = 1
function test() {
  var b = 2
  function inner () {
    var c = 3
    console.log(b) //2
    console.log(a) //1
  }
  inner()
}
test()

//假若我們今天是 JavaScript
inner EC: {
  AO: {
    c: undefined -> 3
  }
  scopeChain: [inner EC.AO, inner.[[scope]]
  = [inner EC.AO, test EC.scopeChain]
  = [inner EC.AO, test EC.AO, globalEC.VO]]
}

test EC: {
  AO: {
    inner: function
    b: undefined -> 2
  }
  scopeChain: [test EC.AO, test[[scope]]]
  = [test EC.AO,  global.VO] //到這邊可以看出來 scopeChain 其實是要傳遞作用域，會一直回推到最外面
}
inner.[[scope]] = test EC.scopeChain = [test EC.AO, globalEC.VO]

global EC: {
  VO: {
    test: function
    a: undefined -> 1
  }
  scopeChain: [global EC.VO]
}

test.[[scope]] = global.VO = global.scopeChain 
//scope 可以看做 test 的作用域，而 scopeChain 則是一個要傳下去做為下一個 function 的作用域 = global.VO
```
### 重新看 closure
- 這邊我們用 scopeChain 的概念重新來解析 closure ，並以一個例子當範例
```javascript=
var v1 = 10
function test() {
  var vTest = 20
  function inner() {
    console.log(v1,vTest)
  }
  return inner
}
var inner = test()
inner()

=====
inner EC: {
  AO: {
  }
  scopeChain = [inner EC.AO, inner.[[scope]]]
  = [inner EC.AO, test EC.AO, global EC.VO]
}
inner.[[scope]] 
= [test EC.scopeChain] 
= [test EC.AO, test.[[scope]]]
= [test EC.AO, global EC.VO]

/* test 執行完後就會釋放資源
test EC: {
  scopeChain: [test EC.AO, test.[[scope]]]
  = [test EC.AO, global EC.VO]
}
test.[[scope]] = global EC.scopeChain = global EC.VO
*/

global EC: {
  VO: {
    v1: undefined -> 10
    test: function
    inner: function
  }
  scopeChain: [global EC.VO]
}

AO: { //雖然 test() 被釋放了，但因為 inner 還保存 AO ，所以必須先留下
  vTest: undefined -> 20
  inner: function
}
```
- 但有時候 closure 的特性會為我們帶來一些麻煩，假如我們在裡面放了一個超大的變數，這個變數在整個程式執行完都不會消失
```javascript=
var v1 = 10
function test() {
  var vTest = 20
  var obj = {superHuge} //因為 scopeChain 這個變數會一直保留
  function inner() {
    console.log(v1,vTest)
  }
  return inner
}
var inner = test()
inner()
```
- 以 scopeChain 的特性來看，因為所有函式資訊都會包含在 AO、VO 裡面，等於所有函式都是 "閉包"

### closure 常見陷阱
- 遞迴，原本想要印出 1~5
```javascript=
var arr = []
for(var i=0; i<5; i++) {
  arr[i] = function() {
    console.log(i)
  }
}

arr[0]() -> 5
=====
var arr = []
var i //先在全域宣告變數
for(var i=0; i<5; i++) {
  arr[i] = function() {
    console.log(i)
  }
}
arr[0]() 
//實際的執行程序
function arr[0]() {
  console.log(i)
}

function arr[1]() {
  console.log(i)
}
...
// 因此最後 i 已經宣告成5，不論我們執行哪個函數都是印出 5
```
- 解決方式之一，是把 var 改成 let 跟之前說的一樣，let 的作用域會儲存在function block裡面
```javascript=
var arr = []
for(let i=0; i<5; i++) {
  arr[i] = function() {
    console.log(i)
  }
}
arr[0]()
=====
var arr = []
for(let i=0; i<5; i++) {
  arr[i] = function() {
    console.log(i)
  }
}
arr[0]()
{
  arr[0] = function () {
    let i = 0
    console.log(i)
  }
}
...
```
- 解決方式之二，是另外寫一個 function 來儲存 i
```javascript=
var arr = []
for(let i=0; i<5; i++) {
    arr[i] = logN(i)
}

function logN(i) {
  return function() {
    console.log(i)
  }
}
arr[0]()
arr[0] = logN(0) //回傳一個新的 function 就可以有一個新的 scope 來儲存 i
arr[1] = logN(1) 
...
```
- 解法三由解法二延伸而來，把 logN 用 IIFE 立即執行來表示
```javascript=
//解法三 IIFE : 立即呼叫 function
(function (num) {
  console.log(num)
})(1234) -> 1234

var arr = []
for(var i=0; i<5; i++) {
  arr[i] = (function(num) {
    let function log() {
      console.log(num)
    }
    return log
  })(i)
}
arr[0]()

```
### 應用
closure 常會用來應用在想把某些變數隱藏或保護起來的情況，讓外部進來的參數無法直接改變原始變數，下面用一個虛擬錢包當例子
```javascript=
// 自製錢包程式
var money = 10

function add(num) {
  money += num
}

function deduct(num) {
  if(money >= 10) {
    money -= 10
  } else {
    if(num < 10) {
      money -= num
    } else {
      return
    }
  }
}

add(1)
deduct(100)
console.log(money)

//但上面的方法會有 money 外洩的問題，也容易被更改，所以可以用 closure 的方式改善，把資料存在 function 裡面
var initMoney = 10
function pocket(initMoney) {
  var money = initMoney
  return {
    add : function add(num) {
      money += num
    },
    deduct : function deduct(num) {
      if(initMoney > 10) {
        money -= 10
      } else {
        money -= num
      }
    },
    getMoney() {
      return money
    }
  }
}

var myPocket = pocket(99)
myPocket.add(10)
myPocket.deduct(6)
console.log(myPocket.getMoney())
```


###### tags: `week16` `closure` `scope chain`