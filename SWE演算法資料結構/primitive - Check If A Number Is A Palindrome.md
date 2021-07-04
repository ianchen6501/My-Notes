### 基本資料
- 判斷回文，例如 "121" return true / "123" return false
- 不能把數字轉換為 string
- 耗時 : 82min

### 上程式碼
```js
const isPalindrome = (x) => {
  //negtive
  if(x<0) {
    return false
  }
  
  let number = x
  let newNumber = null
  let times = 0
  while(number !== 0) {
    if(!newNumber) {
      newNumber = number%10
    } else {
      newNumber = newNumber*10 + number%10
    }
    number = parseInt(number/10)  
  } 
  return x === newNumber? true : false
  
}

```

### 心得
- 這題會考驗到對 integer 操作的技巧
- 對於 Math function 很不熟，基本的 Math.floor / Math.ceil / Math.round / Math.random / Math.pow 等要會用
- Big(O) = O(n)