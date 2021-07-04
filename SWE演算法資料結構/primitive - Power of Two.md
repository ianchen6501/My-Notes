### 題目:
Given a non-negative integer `input`, return `true` if `input` is a power of two. Return `false` otherwise.

### 解題思路:
1. 先轉換為 2 進位，就會變成 '10000' 這種 type，接下來只要判斷是否屬於該 type 就可以
2. 一種是將二進位以 10 為底 log ，如果是正整數就為 powerful 2。但這樣會遇到浮點數誤差的問題。
3. 另外則是把 2 進位減1，判斷兩個位數是否不一樣，但會遇到大數值時的誤差。

### 錯誤解法:
```js
  if(input === 0) {
    return false
  }
  if(input === 1) {
    return true
  }
  //轉換為 2 進位
  const inputBit = Number(input.toString(2))
  
  //透過二進位減一會退一位來判斷是否為
  const num = inputBit - 1
  if((inputBit.toString().length - num.toString().length) === 1) {
    return true
  } else {
    return false
  }
	
	//這個解法會因為 Input 太大，導致顯示的二進位超過安全邊界(2的53次方-1)
	//可以用 isSafeInteger() 來判斷是否為安全邊界內
````

```js
  if(input === 0) {
    return false
  }
  //轉換為 2 進位
  const inputBit = Number(input.toString(2))
  //用 log 10 來判斷
	 function log10 (x) {
	   return (Math.log(x) / Math.log(10)).toFixed(1)
	 }
	 const inputBitLog = log10(inputBit)
	 if(inputBitLog - Math.floor(inputBitLog) !== 0) {
	   return false
	 } else { return true}
	 
//這個解法會在 / Math.log(10) 出現浮點數誤差
```

#### 正確解法
其實可以用第一個解法來解，只是要透過二元運算子，假若是 power 2，power 2 會是 `10000`，那power 2 - 1 會變成類似 `1111` 的形式，那 power2 & power2 -1 會 == 0，就可以用類似下面的方式解
```js
return (input && (input & input -1) == 0)
```
但這樣會有一個問題，如果 input 為 0，那依據  `&&` 運算子的特性如果第一個參數判斷為 false 會回傳參數本身。所以可以透過 `!!input` 或對全體取 `boolean()` 的方式來解決。

### refer
[## [前端工程研究：關於 JavaScript 中 Number 型別的常見地雷與建議作法](https://blog.miniasp.com/post/2020/02/21/JavaScript-Numbers-Deep-Dive)](https://blog.miniasp.com/post/2020/02/21/JavaScript-Numbers-Deep-Dive)