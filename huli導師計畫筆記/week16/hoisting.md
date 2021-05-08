# hoisting

#### 為什麼我們需要 hoisting？
沒有 hoisting 所有宣告的 variable 和 function 都要置頂很麻煩
#### Hoisting 到底是怎麼運作的？
詳見 [ECMAscript Execution Contexts](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-262.pdf)，
裡面大致談到:
> Execution Contexts(EC):
> 每當要執行一個 function 的內部 source code 前會先執行 EC，所有的 function 資訊會存在 EC裡。


> Variable Object(VO):
> 每一個 EC 會有對應的 VO，就像一個 JavaScript 的物件，在進行 EC 時會依序
> 1. 把 參數 放進 EC (參數沒有值的話會存 undefined) 
> 2. 建立 function 的屬性，放入建立 function 完回傳的東西 
> 3. 新增一個 變數 的屬性，並設為 undefined ，如果 VO 已經有該屬性，則值不會被改變。

所以處理流程大概是:
1. 把參數放到 VO 裡面並設定好值，傳什麼進來就是什麼，沒有值的設成 undefined
2. 把 function 宣告放到 VO 裡，如果已經有同名的就覆蓋掉
3. 把變數宣告放到 VO 裡，如果已經有同名的則忽略並維持原本的宣告 

所以下面的程式碼會如此運作
```javascript=
function test(v){
  console.log(v)
  var v = 3
}
test(10)
```
```javascript=
VO
{
v : 10
console.log(10)
}
var v = 10
console.log(10)
var v = 3
```
另一個例子
```javascript=
VO {
  a : undefined
  b : pointer to function
  c : undefined
}
function test(a, b, c) {
  var a = '456'
  function b() {
    consoe.log('789')
  }
  var c = 'c'
}
test(123)
```
### hoisting 是怎麼確實執行的
- 編譯語言 Compiled language
一種程式語言的類型，編譯語言在程式執行前會先透過編譯器(compiler)將程式碼編譯(Compile)成計算機所看的懂的機器碼(machine language)，最後再執行。編譯式語言多半會是靜態語言(static language)，它們會事先定義的型別、型別檢查 (type check) 與擁有高效能的執行速度等特性。
編譯語言— C、C++、bjective-C、Visual Basic等等。
- 直譯語言 Interpreted language
一種程式語言的類型，不同於編譯語言，直譯語言在執行時會一行一行的動態將程式碼直譯(interpret)為機器碼，並執行。直譯語言多半以動態語言(dynamic language)為主，具有靈活的型別處理，動態生成與程式彈性，但速度會比編譯式語言要慢一些。
直譯語言 — JavaScript、Python、Ruby等等。

承上，JavaScript 其實是屬於 直譯語言 ，但這不代表它裡面沒有編譯器的運作，所以也可以理解 hoisting 是可以達到的。

### LHS / RHS
LHS：請幫我去查這個變數的位置在哪裡，因為我要對它賦值。
RHS：請幫我查詢這個變數的值是什麼，因為我要用這個值。

### Time Dead Temporal (TDZ)
var 的賦值在開始後會被設為 undefine(hoisting)，而 let / const 則不會被設為 undefined
```javascript=
console.log(a)
var a = 1 //undefined

console.log(b)
let b = 2 //error

console.log(c)
let c = 2 //error

let d = 10
function test() {
  console.log(d)
  let d = 20
}
test() //error
```
因此在這些變數被確實賦值之前，其實會處在一個 TDZ(temporal dead zone 暫時性死區) 的狀態，在 TDZ 的狀態下如果進行取用會出現錯誤 (strict)
```javascript=
function test() {
    yo() // c 的 TDZ 開始
    let c = 10 // c 的 TDZ 結束
    function yo(){
      console.log(c)
    }
}
test()
```
另一個例子
```javascript=
let a = 10
function test() {
  console.log(a)
  let a = 30
}
test() //error
=====
let a = 10
function test() {
  let a //TDZ 開始
  console.log(a) //error
  a = 30 //TDZ 結束
}
test()
```

### 實例
- 下面是一個提升的案例， test2 會先被宣告，但 function 後面才定義所以在 test2() 這邊就會出現 ``test2 is not a function`` 錯誤
```javascript=
test2()
var test2 = function() {
  console.log(123)
}
---
var test2 //宣告
test2()
test = function() { //復值
  console.log(123)
}
```
- 與這另一個案例不同，這個案例是整個 function 都被提升
```javascript=
test()
function test() {
  console.log(123)
}
---
function test() { //宣告
  console.log(123)
}
test()
```
- 在不同 scope 裡面的 hoisting
```javascript=
var a = 'global'
function test() {
  console.log(a)
  var a = 'local'
}
test()
===
var a
function test() {
  var a
  console.log(a)
  a = 'local'
}
a = 'global'
test() ---> undefined
```
- function 的提升會優先於變數
```javascript=
function test() {
  console.log(a)
  var a = 'local'
  function a() {
    console.log('inner')
  }
}

test()
===
function test() {
  function a() {
    console.log('inner')
  }
  console.log(a)
}

test() -> [function a]
```
- 兩個同樣的宣告，後面的會蓋掉前面的
```javascript=
function test() {
  console.log(a)
  a()
  function a() {
    console.log('1')
  }
  function a() {
    console.log('2')
  }
}
test() -> '2'
```
- 提升的順序， function > argument > var
```javascript=
//function
function test(a) {
  console.log(a)
  function a() {
    console.log(456)
  }
  var a = 789
}
test(123) ---> funciton a
//argument
function test(a) {
  console.log(a)
  var a = 789
}
test(123) ---> 123

1. funciton
2. argument
3. variable
```
- 另一個實例
```javascript=
function test(a) {
  console.log(a)
  var a = 789
  console.log(a)
}
test(123)
======
function test(a) {
  a = 123
  var a
  console.log(a)
  a = 789
  console.log(a)
} 
//123
//789
```





###### tags: `week16` `hoisting`