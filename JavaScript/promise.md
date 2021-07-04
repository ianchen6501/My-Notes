### 基本特性
- 為一個物件基本會包含兩個輸入 resolve、reject 兩個不同處理的函式，
可以看成 
```js
new Promise(successCallback, failureCallback)
```
- 接收到 error 會執行 reject，並會往 promise chain 找尋
- 會確保每一次 .then 非同步的完成



### 一些注意事項
- 基本上所有的非同步都會回傳 promise ，但 setTimeout 等古典方法為例外，所以如果要用 promise chain 處理要用 promise 包起來。

### promise.resolve(value)
Promise.resolve等於是要產生 fulfilled(已實現)狀態的 Promise 物件，它相當於直接回傳一個以then方法實現的新 Promise 物件，帶有傳入的參數值，這個方法的傳入值有三種:
```js
Promise.resolve(value);
Promise.resolve(promise);
Promise.resolve(thenable);
```
也就是除了用建構式的new Promise()外，提供另一種方式來產生新的 Promise 物件。


### codepen
<iframe height="300" style="width: 100%;" scrolling="no" title="Async/await &amp; Promise" src="https://codepen.io/ianchen6501/embed/BaRaeGR?defaultTab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/ianchen6501/pen/BaRaeGR">
  Async/await &amp; Promise</a> by ian5555 (<a href="https://codepen.io/ianchen6501">@ianchen6501</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

### reference
[Promise.resolve 與 Promise.reject](http://promise.eddychang.me/docs/contents/ch7_promise_resolve_n_reject/)