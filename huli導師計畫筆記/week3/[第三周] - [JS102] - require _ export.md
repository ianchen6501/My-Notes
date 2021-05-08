# [第三周] - [JS102] - require / export
### require : 把 module 引入專案
```javascript=
var 代稱 = require('module_name')
console.log(module_function())
```
### export : 創造一個 module 給別人用
1. 先寫一個 module export
```javascript=
function double(n){
    return n*2
}
module.exports = double // 表示 double 要輸出 module 給別人用
```
2. 在別的檔案引入 require
```javascript=
var double = require('./double') 
// require 後面要輸入檔案位址 ./module_name
console.log(double(5)) => 10
```
3. module 也可以寫成 object 就可以有多個輸出方法
```javascript=
function double(n){
    return n*2
}
function triple(n){
    return n*3
}

var obj ={
    double : double,
    triple : triple
}

module.exports = obj
```
```javascript=
var double = require('./double')
console.log(double.double(5),double.triple(6))=> 10,18
```
4. 另一種寫法
```java=
function double(n){
    return n*2
}
function triple(n){
    return n*3
var mymodule = require('./mymodule')
console.log(mymodule) => Object {double: , triple: }
console.log(mymodule.double(5))
}

exports.double = double
exports.triple = triple
```
```javascript=
var mymodule = require('./mymodule')
console.log(mymodule) => Object {double: , triple: }
console.log(mymodule.double(5)) => 10
```
5. 比較上述兩種寫法，' exports.double = double '輸出的一定是一個 obj ，但' module.exports = obj '可以輸出 arr , str , obj 等

###### tags: `week3`