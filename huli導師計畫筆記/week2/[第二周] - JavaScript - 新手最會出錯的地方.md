# [第二周] - JavaScript - 新手最會出錯的地方
- console.log 會印出取到的值，常用來偵錯，錯誤的使用例子如下
```javascript=
function add (a,b){
	console.log(a+b) // 印出 a+b
}
console.log(add(1,2)) //先執行 add(1,2) 然後印出 function 的回傳值 undefined
3
undefined
```
- return : function 的回傳值，正確的寫法如下
```javascript=
function add (a,b){
	return a+b 
}
console.log(add(1,2))
```
- browser 的 console.log 會自動產生 undefined 其機制與 node.js 不同不用過於在意

### immutable 不可變性
- 大觀念: 除了 object , array 外大部分的元件(number / string ...)都是 immutable 的(
- 物件內容不會被改變。
- 例如說今天 var 了 a ，然後再做一次 var ，第二次的賦值其實沒有改變原本第一次記憶體位置的內容，而是在一個新的記憶體位置重新放入新的內容。
```javascript=
var a = 1 //存在記憶體位置 0x01
a = a +2  //存在記憶體位置 0x02
console.log(a) => 1
```
```javascript=
var a = "hello"
function change(str){
	str = "123"
}
change(a)
console.log(a) =>"hello"
```
- 如果要變更原本位置的內容，要重新對其賦值
```javascript=
var a = 'hello'
var a = a.split('')
console.log(a)
'h,
e,
l,
l,
o'
```
- 但針對 array / object 等不是 immutable 的物件，某些 function 會直接改變該記憶體位置的內容。
```javascript=
var a = [1,2,3]
a.push(4)
console.log(a) 
[1,2,3,4] 
```
- 針對上例，新手如我會有一個錯誤的寫法
```java=
var a = [1,2,3]
a = a.push(4)
console.log(a) 
[1,2,3,4] 
4 
/* 為何會有這樣的結果，先看 .push MDN 的解釋"push() 方法會添加一個或多個元素至陣列的末端，並且回傳陣列的新長度。"
所以上面 a = a.push(4)其實做了兩件事情，一個是在 a array 裡面新增了一個 '4' 然後回傳了 length 。所以 console.log() 的結果其實是 array length = 4
```
- push / splice / reverse / sort / shift / unshift ... 等編輯 function 會有相同特性
- slice 會回傳一個新的 array ， join 會回傳一個 string 等，所以要注意回傳值及會不會更動原本的記憶體位置。
- 總結:
1. 如果是會修改原本的內容，就不能用重新賦值的方式
2. 而如果是 string / number 等 immutable 物件就必須要給他一個新的賦值。
3. 另外有一種像 push 是會修改而且回傳一個新的值就要特別注意。

### debug 神器 - 請善用 console.log()
```javascript
function isPrime(a){
    console.log('a:',a) //debug
    if(a === 1){
        return false
    } 
    if(a === 2 ){
        return true
    }
    for(var i=2; i<a; i++){
    console.log('i',i)
        if(a%i === 0){ 
            return false
        }
        else{
            return true // 在 i = 2 時回傳 true，應該要在所有的 i 的可能性都確認完後再執行 return true
        }
    }
}

console.log(isPrime(15))
// 下面是回傳值
"a:", 15
"i", 2
true
```
```javascript
function isPrime(a){
    console.log('a:',a) //debug
    if(a === 1){
        return false
    } 
    if(a === 2 ){
        return true
    }
    for(var i=2; i<a; i++){
    console.log('i',i)
        if(a%i === 0){ 
            return false
        }
                else{
            return true
    }
}
}
console.log(isPrime(15))

```
###### tags: `week2`