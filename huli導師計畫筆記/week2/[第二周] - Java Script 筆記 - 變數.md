# [第二周] - Java Script 筆記 - 變數
### 變數 (variable) 簡介
- 可以想像變數是一個盒子，盒子裡我們可以給他放任何東西，之後只要提到盒子就等於裡面的東西。
- 在盒子裡面放東西的過程就是賦值，賦值在 java script 的做法如下
```
var box = 1
```
- 變數定義大小寫是不同的東西， var abc =/= var ABC
- 如果今天定義一個變數卻不給他值的話，會顯示 "undefined"
```
var box 
console.log(box)
undefined
```
- 變數命名不能用數字及保留字開頭
- 變數的命名原則，1. 底線式 (I_love_you)、2.駝峰式(ILoveYou)
- 變數可以重複的賦值
```
var a = 1
var a = a + 1
console.log(a) 
1
```
- 變數的運算簡寫
a = a + 1 => a += 1 => a++ => ++a
a = a - 1 => a -= 1 => a-- => --a
```
var a = 1
a += 2
console.log(a)
3
var b = 2
b--
console.log(b)
1
```
- 變數的 "a++" 和 '++a' 的運算順序會不同， 前者會先執行外部函數再執行， 後者會先執行完再執行外部函數
```
var a = 0 
console.log(++a && 50) #第一種情形
=>
1. a += 0
2. console.log

ocnsole.log(a++ && 50) #第二種情形
=>
1. console.log
2. a += 0
```
### 變數的類型
- primitive - boolyn / number / string 
- object / undefined / function
- 判斷變數的類型: typeof +variable

### 陣列 array
- 陣列是用來處理同類型的不同項目用，通常會搭配迴圈 for
- 宣告陣列: var a = [ ] 
- 陣列的長度: a.lenth
- 增加陣列內的項目: a.push(增加的項目) / a[a.length] = 增加的項目

### 項目 Object
- 如果同時要處理多個不同類型的項目，如班級同學的資訊(電話、地址...)，如果要把不同類型分開編列，會十分的麻煩，這時候就需要用 Object 來處理。
- 宣告項目(object): var a = {key:value}

```javascript=
var c = {
"name":"ian"
"phone":"0968895225"
"class":"6C"
}
```
- 提取項目內容的方式
variable 後面加 .key 或 [key] ，也可以透過混用的方式把 arry push object 裡面在提取出來
```javascript=
var a = []
var ian = {
girlfr : "emily"
company : "fpg"
car : "jupy"
}
a.push(ian)
console.log(ian.girlfr) => emily
console.log(ian['company']) => fpg
console.log(a[0].car) =>jupy
```
- object 的巢狀結構
```javascript=
var anderson = {
class : "6C"
country : "Taiwan"
City : "Taipei"
moterh : {
name : "Arisa"
}
}
console.log(anderson.mother.name) => arisa
console.log(anderson['mother']['name']) => arisa
```
- 變數運算的注意事項
注意型態，例如如果是 intiger + string JavaScript 會自動判斷 intiger 為 string 然後出現錯誤，例子如下。
```javascript=
var a = '10'
var b = 20
console.log(a+b) =>1020
```
解決的方式是在 string 前面加 function - number() 或 parseInt()，範例如下:
```javascript=
var a = '10'
var b = 20
console.log(number(a)+b) =>30
console.log(parseInt(a,10)+b) => 30 #parseInt(變數,進位法)
```
另外要注意浮點數誤差，如果是小數點，在 javaScript 不會儲存正確的小數，後面會有極小的誤差，這樣在運算時就會出現錯誤。

- 程式運算順序
程式運算一般都是由右到左，例如:
```javascript=
console.log(10=="10") => True
10=="10" //先運行
console.log(True) //後運行
```

- = 為賦值、== 判斷值不判斷型態、=== 判斷值也判斷型態(建議在一般的時候盡量使用 === )
```javascript=
var a = 10 //賦值
console.log(10 == "10") => True
console.log(10 === "10") => False
```

- array 或 object 賦值時儲存的是記憶體位址而非程式碼的內容。所以在判斷時會出現下列情形。
```javascript=
console.log([] == []) //false
console.log({} == {}) //false
console.log([a] == [a]) //false
console.log({a:1} == {a:1}) //false
```

- 為何會出現上述的情形，要理解 array 跟 obj 對應的是一個記憶體位址，所以其實可以有多個 array(obj) 同時對應一個記憶體位址。
```javascript=
var a = []
var b = a //a 跟 b 對應同一個位址
```
- 除非我們重新賦值(改變位址)，才會變更連結。不然如同上例，如果變更了 a 那 b 也會一起改變。
```javascript=
var a = [1]
console.log(b) = [1]
```
![](https://i.imgur.com/5W04oeX.png)
![](https://i.imgur.com/lV9N1HE.png)

###### tags: `week2`


