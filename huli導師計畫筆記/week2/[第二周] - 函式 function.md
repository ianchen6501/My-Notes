# [第二周] - 函式 function
- function 基本語法
```javascript=
function 函式名稱(變數,變數,變數){
函式內容 // return...}
```
- 執行 function
```javascript=
console.log(funcion(變數))
```
- 練習:列出 1~n 個數列
```javascript
function generatearray(n){
	var array1 = []
  for(var i = 1 ; i <= n ; i++){
  array1.push(i)
  }
  return array1
}
console.log(generatearray(20))
```
- 練習:列出偶數
```javascript=
function even(n){
  var numarray = []
  for(var i = 1 ; i <= n ; i++){
    if(i%2 === 0){
    numarray.push(i)}
  }
  return numarray
}
console.log(even(20))
```
- 變數是可以輸入函式結果的，做出比較複雜的運算
```javascript
function print(anything){ //anything 變數輸入函式的結果
	anything()
}
function hello(){ //預備的函式
	console.log('hello')
}
print(hello)
```
- 練習:變數輸入函式，以 array double 為例
```javascript=
function arraydouble(arr,transformfunction){
  var result = []
  for (var i=0; i<arr.length ; i++){
  	result.push(transformfunction(arr[i]))
  }
  return result
}
function double(n){
	return n*2
}
console.log(arraydouble([2,4,6],double)
)
```
- annonymous function 匿名函數
```javascript=
function arraydouble(arr,transformfunction){
  var result = []
  for (var i=0; i<arr.length ; i++){
  	result.push(transformfunction(arr[i]))
  }
  return result
}
console.log(arraydouble([2,4,6],function(x){
	return x*2 //直接把上例的 double function 放進來，免取名
})
)
```
- parameter 參數 vs argument 引數
1. parameter 參數是 function 語法裡 ()裡的代數
```javascript=
function 123(a,b,c) // a.b.c 就是代數
```
2. arguments 引數是實際在函式裡運算的代數
```javascript=
function 123(a,b,c){
return a+b+b
}
123(4,5,6) //4.5.6 就是引數
```
- 查詢引數的功能 function arguments (類陣列)
透過在函式裡面放 argument 可以回傳實際的引數
```javascript=
function add(a,b){
console.log(arguments)
return a+b
}
console.log(5,7)
=> {5:7 , 1,7} 
// 其中 arguments 是一個 object(類陣列) 而非 array，所以他可以有length 
```
- 使用 function 時的注意事項
在[JS101]-"從 Object 的等號真正的理解變數"裡面有提到如 object / array 等物件或陣列其實是儲存在一個記憶體空間，而 boolyn 、 number 等簡單的物件則是以一個值在傳遞和儲存，因此如果在用 function 處理 object 時可能會遇到結果與想像不一致的問題
```javascript=
function swap(a,b){
/*
var a = n1 ... 複製了一個 n1 的值
var b = n2 ... 複製了一個 n2 的值
 */
temp = a
a = b
b = temp
console.log('a,b:',a,b) 
}
var n1 = 10
var n2 = 20
console.log(n1,n2) =>10,20 // 回傳原本n1,n2記憶體位置的內容

swap(n1,n2)=> a,b: 20,10 // 回傳複製的值

```
- 另外要注意，有兩種狀況一種是去改變 obj 裡面的值或建立一個新的 obj 連結，另外一種是重新賦值後就會對應到新的記憶體。
1. 改變 obj 的值:
```javascript=
var obj = {a:1}
obj.a => 會去改裡面的值
var obj2 = obj
obj2.a => 會更改到 obj 裡的值
```
2. 重新賦值
```javascript=
var obj2 = {b:1} => 會建立一個新的記憶體位置

```
- 上面提到的事情其實有三種狀況，有空可以深入研究
1. pass by value
2. pass by reference
3. pass by sharing
[深入探討 JavaScript 中的參數傳遞：call by value 還是 reference？](https://blog.techbridge.cc/2018/06/23/javascript-call-by-value-or-reference/)

- return 的意義
function 其實可以分為兩種。1. 不要求回傳值，所以可以只印出我要的結果(例如 print hello world)，2. 要求回傳值。所以對於 function 來說 return 後面就是這個函式的回傳值，當執行到 ruturn 時就會跳出 function 並回傳值。
```javascript=
function printhello(name){
    console.log('hello ',name)
}
```
```javascript=
function trible(n){
return 3*n //會執行
console.log(3*n) // 不會執行
}
```
```javascript=
function trible(n){
return 3*n 
}
var result = double(3)
console.log(result) =>9
```
```javascript=
function trible(n){
console.log(3*n) 
}
truble(3) =>9 //會直接印出

```
###### tags: `week2`
