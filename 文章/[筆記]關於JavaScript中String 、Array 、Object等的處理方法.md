## 型別

- 原始型別(primitive)：

  > Boolean
  > Null
  > Undefined
  > Number
  > BigInt
  > String
  > Symbol（於 ECMAScript 6 新定義）

- Object

## 深淺拷貝

---

## 字串的處理方法(methods)

### 字串拼接

> 字串可以透過 "+" 或 "+=" 來拼接，會接在該字串的尾端，這邊要注意如果要刪節字串的話可以用 `.split()`

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

### split

`.split([seperator, [limit]])`

> 可以將字串透過 seperator 分割成陣列，並且可以傳入第二個參數限制陣列的數量，到達數量後就停止。

```js
let string = "a,b,c,d,e,f";
const arr = string.split(",", 3);
console.log(arr); //[a,b,c]
```
