# [第二周] - JavaScript - Number 常用的內建函式
- 內建函式: 程式語言內建的 function ，可以幫助節省時間與讓 code 更簡潔。
- 常用的參考資料
[mozila](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Number)

- Number(string) : 把字串轉換成數字
```javascript=
console.los(10 + Number('20.5'))
30.5
```
- parseInt(string ,進位法) : 也是把字串轉換成數字但可以選擇進位法
```javascript=
console.los(10 + parseInt('20.5',10))
30.5
```
- parseFloat(stirng).toFix(要進位的點數) : 主要用來處理浮點數轉換成數字
```javascript=
console.los(10 + parsefloat('20.55'))
30.6
```
- Number.MAX_VALUE : JavaScript 可以處理到精準的數值範圍
```javascript=
console.log(Number.MAX_VALUE)
1.7976931348623157e+308
```
- Math.PI : 印出圓周率
```javascript=
console.log(Math.PI)
3.141592653589793
```
- Math.ceil : 無條件進位
- Math.floor : 無條件捨去
- Math.round : 四捨五入
```javascript=
console.log(Math.ceil(20.1)) => 21
console.log(Math.floor(20.1)) => 20
console.log(Math.round(20.1)) => 20
```
- Math.sqrt : 開根號
```javascript=
console.log(Math.sqrt(20))
4.47213595499958
```
- Math.max : 取最大值
```javascript=
console.log(Math.max(20,10,30,100))
100
```
- Math.min : 取最小值
- Maht.pow(初始值,次方) : 取次方
```javascript=
console.log(Math.pow(2,6))
64
```
- Math.random : 產生 0 至 <1 中間的數值
```javascript=
//產生 1-10 之間的整數
console.log(Math.floor(Math.random()*10))
```
- .toString() : 產生字串
```javascript=
var a = 10 
console.log(a.toString())
'10' // 方法一

var b = (10 + '20') 
console.log(b)
'1020' // 方法二
```
###### tags: `week2`