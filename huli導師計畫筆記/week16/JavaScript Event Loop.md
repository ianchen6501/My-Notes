# JavaScript Event Loop
### V8 Runtime
#### Overview
> a runtime or runtime environment contains the JavaScript engine that parses and executes script code. The runtime provides rules for how memory is accessed, how the program can interact with the computer's operating system, and what program syntax is legal. Each web browser has a runtime environment for JavaScript.

1. JavaScript 執行引擎。
2. 可以解析跟執行 Script code。
3. 瀏覽器內有自己的 runtime 引擎。

#### big structure
<img src="https://i.imgur.com/i7DVvFZ.png" height=80% width=80%/>

### 引言
- Settimeout / DOM / http / Callback request don't exist in V8
- JavaScript 是一個單執行序語言

### 名詞解釋
- heap : 堆疊，泛指記憶體中的一個無結構區域
- queue : 佇列，webAPI 待處理的訊息，會由 eventLoop 協助排程
- call stack : 堆積，當 JavaScript 在執行函數時，其實也跟變數一樣有分為全域執行與部分執行，也時常會有 A 函式內包含 B 函式等情形，所以 JavaScript 透過 call stack 的方式來判斷函式執行的順序。
<img src="https://i.imgur.com/KVV6unJ.png" height=50% width=50%/>
- blocking : things are slow
- Asynchronous Callback : 非同步，多執行序，多個事件時不會因為線性執行而卡住
- callback - Asynchronous Callback
- 每秒 60 楨
- render queue

### EventLoop 的現象
來看一個例子
```javascript=
console.log('hi')
setTimeout(() => {
console.log('5 secs'), 5000
})
console.log('bye')
-> 'hi'
-> 'bye'
-> '5 secs'
```
一開始的時候因為 JavaScript 單執行序的特性，會馬上印出 hi ，接著執行 setTimeout 但因為 SetTimeout 不會馬上執行 callback 所以會執行(沒有發生任何事)後然後繼續下一行，印出 bye ，等 5 秒後就印出 5 secs。那 Event Loop 就是讓瀏覽器可以在 5 秒後印出 5 secs 的機制。

所以我們可以知道，像是 setTimeout / Ajax / callback 這些機制其實是在 V8 runtime 之外，是瀏覽器額外提供的 webapi ，當 JavaScript 處理到這些任務的時候其實會把這些丟到 webAPI 去處理，這時候瀏覽器就可以繼續執行下一步。等到 webAPI 執行完成後，這些任務會被丟到 taskList ，然後 EventLoop 這時候就發揮作用了，EventLoop 會把這些在 taskList 的任務排進 JavaScript 的工作流程中，所以上一段提到的 setTimeout 就會 console.log 出 5 secs 了。
<img src="https://i.imgur.com/qMGshax.png" height=50% width=50%/>

### 回過頭來談怎麼不阻塞 blocking
應該是要盡量減少大量同步的事件，不然瀏覽器就會卡在那邊，什麼都不能做。
另外因為瀏覽器的顯示(render)優先層級大於 callback ，所以如同上述所說的，如果我們在 call stack 執行一些很慢的動作(如delay())，會造成瀏覽器的顯示被卡住。










###### tags: `week16` `JavaScript` `EventLoop`