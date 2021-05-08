# scope 作用域 (before ES6)
### local variable 區域變數
僅在 function 內作用
```javascript=
function loga() {
  let a = 20
  console.log(a)
}
```

### global variable 全域變數
在整個檔案裡運行的變數
```javascript=
var b = 10
function logb() {
  console.log(b)
}
logb()
console.log(b) //10
```
記得要對變數賦值(var)，避免出現沒有用 var 的情況，這樣會變成全域變數，global variable 一多就容易衝突

### scope chain
如果在當層找不到賦值的話，js runtime 會自動往上找
```javascript=
var a = "global a"
function test () {
  var a = "test a"
  var b = "test b"
  console.log(a, b)
  function inner () {
    var b = "inner b"
    console.log(a, b)
  }
  inner()
}
test()
console.log(a)

inner b -> test b -> global
```

### scope chain 的常見錯誤理解
scope 應該看 function 定義的位置，而非被引用的位置，如下例 test 的 scope 應該是 ``test() -> global``
```javascript=
var a = "global" //gloabal scope
function change() { //local scope - change
  var a = 10
  function inner () {
    var a = "inner"
    test()
  }
  inner() //local scope - test
}

function test() { //local scope - test
  console.log(a) 
}
change()

```

### var / let / const
var : scope -> function
let / const : scope -> block

###### tags: `week16` `scope`