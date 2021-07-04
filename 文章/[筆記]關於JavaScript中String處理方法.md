### 型別
- String 屬於 primitive，常見的 primitive 如下。
  > Boolean
  > Null
  > Undefined
  > Number
  > BigInt
  > String
  > Symbol（於 ECMAScript 6 新定義）
- primitive 的特性是 pass by value ，意思是當我們再複製一個 primitive 的時候複製的是他的值而非記憶體位置。
- 
- ㄧ般透過 `""` 建立的 string type 是 `string`，但透過 `new String("text")` 則是 object，所以 `"string" == new String("string")`會得到 `true` 而 `"string" === new String("string")` 則是 `false` 因為型別不同

## 字串的處理方法(methods)

### 字串拼接

> 字串可以透過 "+" 或 "+=" 來拼接，會接在該字串的尾端，這邊要注意如果要刪節字串的話可以用 `.split()`

### 字串跳脫
> 如果遇到特殊字元，字串可以透過 `\` 來跳脫
```js
console.log("\"ian\") //"ian"
```

### length

> 可以取得字串長度

```js
const string = "yoyo";
console.log(string.length); //4
```

### indexOf
> 可以檢查字串中是否包含某些字元組合，如果有會回傳第一個符合條件的位址，沒有澤會回傳 "-1"

```js
const string = "yoyo"
console.log(string.indexOf("yo")) //0
console.log(string.indexOf("ya)) //-1
```

> 也可以應用在 array
`arr.indexOf(searchElement\[, fromIndex\])`
第一個參數傳要搜尋的 value ，後面傳開始的位置(輸入負值會從最後一個開始倒數到指定位置由左往右搜尋)
```js
const array = [1, 2, 3, 2, 4, 2]
console.log(array.indexOf(2)) //2
console.log(array.indexOf(7)) //-1
console.log(array.indexOf(2, 2)) //3
console.log(array.indexOf(2, 6)) //-1
console.log(array.indexOf(2, -3)) //3

//找尋所有出現的
var arr = ["a", "c", "d", "y", "a"]
var indices = []
var element = "a"
var idx = arr.indexOf(element)
while(idx != -1) {
  indices.push(idx)
  idx = arr.indexOf(element, idx +1)
}
console.log(indices) //[0,4]
```

### split

`.split([seperator, [limit]])`

> 可以將字串透過 seperator 分割成陣列，並且可以傳入第二個參數限制陣列的數量，到達數量後就停止。

```js
let string = "a,b,c,d,e,f";
const arr = string.split(",", 3);
console.log(arr); //[a,b,c]
```

### slice

### replace
 string 中的文字置換
 ```js
 var str = 'hey yo man how are you?'
console.log(str.replace('hey','!!!'))
'!!! yo man how are you?'
//但要注意只會置換第一組字元，後面的還會保留，如果要全部置換要改成 正規表達式(RegExp)
 ```

### trim
把"前後"的空格去掉
```js
var str = '   i am a boy   '
var strtrim = str.trim()
console.log(strtrim)
'i am a bou'
```

### toUpperCase
將 string 改成大寫
### toLowerCase
將 string 改為小寫
### charCodeAt
找出字母的 UTF-16代码单元 (0-65535)
### fromCharCode
把代碼轉變為字母
```js
var a = 'n'.charCodeAt()
console.log(a) // i =>105, I => 72 中間相差32
//要把 n 轉成大寫, n=>110 --- N = n-32 = 68
var str = String.fromCharCode(78)
console.log(str)
'N'
```
