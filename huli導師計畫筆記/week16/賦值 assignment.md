# 賦值 assignment
### primitive type
會直接存值，所以假設今天 ``var b = a`` 改變 b 的值的時候，a 不會改變
```javascript=
a : 10
b : 10
-> b : 20

var a = 10
var b = b
console.log(a, b)

var b = 20
console.log(a, b)
```

### object
會對賦值的對象存記憶體位置，所以假設今天 ``var b = a``
等於指定 a 的記憶體位置給 b，今天如果有用 .push 或 .number 等方法改 a 的話，b 也會跟著改變
```javascript=
/*
0x10 : ['arr2']

arr: 0x10
arr2: 0x10
*/

var arr = []
var arr2 = arr
console.log(arr, arr2)

arr2.push('arr2')
console.log(arr, arr2)

//obj
var obj = { number: 10}
var obj2 = obj
console.log(obj, obj2)

obj2.number = 20 //.number 是改到那個記憶體位置的性質，跟 .push 一樣
console.log(obj,obj2)
```
但有另一種狀況，如果今天是對 b 給一個新的記憶體位置，那 a,b 記憶體位置不同，就不會互相影響
```javascript=
var arr = []
var arr2 = arr
console.log(arr, arr2)

var arr2 = [4, 5, 6]
console.log(arr, arr2)

//obj
var obj = { number: 10}
var obj2 = obj
console.log(obj, obj2)

var obj2 = { number: 20}
console.log(obj,obj2)
```


###### tags: `week16` `assignment`
