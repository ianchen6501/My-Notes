### 常見的 closure 的現象
當我們在 function 裡回傳一個 function 並且在函式外透過函式宣告的方式去執行，會發現儘管函式已經執行結束，函式裡面的變數卻不會消失。
```js
let money = 10
const closure = function() {
  return function(n) {
    money += n
    console.log(money)
  }
}

let myMoney = closure()
myMoney(1) //11
myMoney(2) //13
```
這個現象就叫做閉包，至於要理解為什麼會這樣必須先得了解幾個概念。

### execution context
- 執行程式碼的地方，分為全域和函式兩種。
- 最外層的會是全域的環境(global execution context)，當遇到函式要執行的時候就會創建一個新的函式環境並且進入新的環境中執行。
```js
const a = 1 //全域執行環境
function echo() {
	const b = 2
	console.log(a, b) //函式執行環境
}
```
執行環境的建立有兩個階段，`建立`和`賦值`階段
#### 建立階段
1. 建立 scope chain
2. 建立 variable object / activation object，依序建立參數、函式(pointer 指向記憶體位置)、變數(undefined)等
3. 建立 this
#### 執行階段
一行一行執行程式碼及賦值等。

#### variable object / activation object
每個執行環境裡面會有一個 object 包含`參數`、`函式`、`變數`等基本資訊，在全域環境叫 variable object 、在函式環境較 activation object。
創建 V.O 或 A.O 的過程其實就是 hoisting 宣告的過程，順序如下
1. 參數，有值就宣告值沒有就是 undefined
2. 函式，宣告一個 pointer 指向某個記憶體位置，如果原本有同名的函式會覆蓋過去。
3. 變數，如果有就維持原本的值，沒有就新增 undefined

#### scope chain

#### garbage collector(G.C)
前面有提到，函式執行結束的時候基本上裡面的 A.O 其實也會被釋放或消失，這個其實是 garbage collector 在做的事，GC 就是一種記憶體管理機制，當函式執行完畢時，就會把儲存函式的記憶體給釋放出來。
常見的記憶體釋放演算法有兩種。
> `Reference counting`
> 會掃除掉那些沒有被引用的記憶體。但會漏掉循環參考的狀況如
> ```js
> function() {
>   let obj1 = {}
>   let obj2 ={}
>   obj1.a = obj2
>   obj2.a = obj1
>   console.log(obj1)
> }
> ```

> `Mark-and-Sweep`
> 找出那些從 varibla object 無法到達的物件


---
### 更深談 closure
closure 其實就是一個特殊的函式而且不會被 GC 給回收，他紀錄了自己及外層 EC 的 AO.VO 資訊。

### 更多應用

### reference
[記憶體管理-mdn](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Memory_Management)
[理解 Javascript 執行環境](https://andyyou.github.io/2015/04/18/what-is-the-execution-context-in-javascript/)
[參透Javascript閉包與Scope Chain](https://andyyou.github.io/2015/04/20/understand-closures-and-scope-chain/)