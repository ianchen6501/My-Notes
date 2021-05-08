# [第二周] - JavaScript String 的內建函數
- toUpperCase 將 string 改成大寫
- toLowerCase 將 string 改為小寫
```javascript=
console.log('b'.toUpperCase())
'B'
console.log('b'.toLowerCase())
'b'
```
- .charCodeAt(字母位置): 找出字母的 UTF-16代码单元 (0-65535)
- .fromCharCode : 把代碼轉變為字母
```javascript=
var a = 'n'.charCodeAt()
console.log(a) // i =>105, I => 72 中間相差32
//要把 n 轉成大寫, n=>110 --- N = n-32 = 68
var str = String.fromCharCode(78)
console.log(str)
'N'
```
- string 是可以比大小的
```javascript=
var char = 'd'
console.log(char >= 'b' && char >= 'c')
true
```
- indexOf('要搜尋的字元組合'):  會顯示在 string 內要搜尋的字元組合位置，尋找不存在的會回傳負數
```javascript=
var string = 'hey yoyo man!'
var index = str.indexOf('man')
console.log(index)
9
```
- replace('要被換掉的字母','準備取代的字母') : string 中的文字置換
```javascript=
var str = 'hey yo man how are you?'
console.log(str.replace('hey','!!!'))
'!!! yo man how are you?'
//但要注意只會置換第一組字元，後面的還會保留，如果要全部置換要改成 正規表達式(RegExp)

```
[正規表達式](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Regular_Expressions)
```javascript=
var str = 'hey yo man how are you?'
console.log(str.replace('/y/g','!'))
'!o man how are !ou?'
```
- split('seperator') : 把 string 分割成 array
```javascript=
var str = 'data1,data2,data3,data4'
var strsplit = str.split(',')
console.log(strsplit)
["data1", "data2", "data3", "data4"]
```
- trim : 把"前後"的空格去掉
```javascript=
var str = '   i am a boy   '
var strtrim = str.trim()
console.log(strtrim)
'i am a bou'
```
- .length : 求取 string 長度，注意他不是 function 後面不會有()
```javascript=
var str = "scienst"
for(var i=0; i<str.length; i++){
	console.log(str[i])
}
"s"
"c"
"i"
"e"
"n"
"s"
"t"
```

###### tags: `week2`