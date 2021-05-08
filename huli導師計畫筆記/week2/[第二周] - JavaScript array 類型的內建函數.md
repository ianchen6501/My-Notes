# [第二周] - JavaScript array 類型的內建函數
### Join : 把陣列的 elements 結合在一起
```javascript=
var arr = ['我','愛','你']
console.log(arr.join('!'))
```
### map : array 運算後回傳一個新的 array
語法如下: variable.map(function)
```javascript=
var arr = [1,2,3]
function double(n){
	return n*2
}
console.log(arr.map(double)) => [2,4,6]
console.log(double(arr)) //錯誤
```
```javascript=
var arr = [1,2,3]
console.log(arr.map(function(n){
	return n*2
})) //anonymous function
```
### filter : 過濾回傳值
```javascript=
var arr = [1,2,3,-1,5]
console.log(arr
    .map(function(n){
    return n*2
    }
    .filter(function(n){ // 注意arr後面的 function 可以串接
    return n > 0
    })
))
[2, 4, 6, 10] 
```
### slice : 切割出你想要的 array(不影響原本的 array)
語法: arr.slice(begin,end)，包含 begin / 不包含 end
```javascript=
var arr = [1,2,3,-1,5]
arr.slice(0,2)
```
### splice : 插入或刪除 array(會更動原本的 array)
語法: array.splice(start[, deleteCount[, item1[, item2[, ...]]]])
```javascript=
var myFish = ['angel', 'clown', 'mandarin', 'sturgeon'];
var removed = myFish.splice(2, 0, 'drum')
// myFish 為 ["angel", "clown", "drum", "mandarin", "sturgeon"] 
// removed 為 [], 沒有元素被刪除
\
```
### sort : array 的排序 (會改變原 array)
- 排序 number
```javascript=
var arr = [3,4,2,6,1]
var arrsort = arr.sort()
console.log(arrsort)
[1,2,3,4,6]
```
- 排序 string (依照string 裡面第一個 elements 來排序)
```javascript=
var arr = [20,15,30,3,12,0,1]
var arr.sort = arr.sort()
console.log(arrsort)
```
```javascript=
var arr = [1,30,4,21]
var arrsort = arr.sort()
console.log(arrsort)
[1, 21, 30, 4]
```
- 自訂排序規則
語法 : arr.sort([compareFunciton])
1. 若 compareFunction(a, b) 的回傳值小於 0，則會把 a 排在小於 b 之索引的位置，即 a 排在 b 前面。
2. 若 compareFunction(a, b) 回傳 0，則 a 與 b 皆不會改變彼此的順序，但會與其他全部的元素比較來排序。備註：ECMAscript 標準並不保證這個行為，因此不是所有瀏覽器（如 Mozilla 版本在 2003 以前）都遵守此行為。
3. 若 compareFunction(a, b) 的回傳值大於 0，則會把 b 排在小於 a 之索引的位置，即 b 排在 a 前面。
4. compareFunction(a, b) 在給予一組特定元素 a 及 b 為此函數之兩引數時必須總是回傳相同的值。若回傳值不一致，排序順序則為 undefined。
```javascript=
var arr = [1,30,4,21]
var arrsort = arr.sort(
	function(a,b){ //由小到大
  if(a > b) {
  	return 1
    }
  if(a < b){
  	return -1
    }
  return 0
  }
  )
console.log(arrsort)
[1, 4, 21, 30]
```

###### tags: `week2`












