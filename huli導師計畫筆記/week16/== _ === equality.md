# == / === equality
### ==
會對判斷的兩個值做型別轉換後才進行判定，所以比較不精準，例如 ``'1' == 1 -> true``

### === 
會同時判斷型別、數值。但要注意對於 primitive type / object 兩個判斷的基準是不同的，primitive type 比對的是值，object 則是記憶體位置。
```javascript=
console.log(1 === '1') //false
console.log([] === []) //false
console.log({} === {}) //false

var a = {number : 10}
var b = a
console.log(a === b) //true
```

### special case : NaN
NaN 不等於任何東西， typeof NaN === number
```javascript=
console.log(NaN === NaN) //false

var a = Number('hello') 
console.log(a === a) //false

```

[JavaScript Equality](https://dorey.github.io/JavaScript-Equality-Table/)

###### tags: `week16` `equality`