# [第三周] - lidemy OJ 簡介含輸入介紹
### OJ = Online Judge System
### 分為兩種類型
1. 實作 function :  
直接寫 function 的內容，並用 return 輸出
3. 檔案 i/o
用 input 標準輸入，然後用 console.log 輸出

### 基本的 i/o 架構
```javascript=
var readline = require('readline');
var rl = readline.createInterface({
    input: process.stdin
})
//設定 readline 標準輸入
var lines = []
rl.on('line', function (line){
    lines.push(line)
});
//把輸入的資料放入一個 arr ，按 ctrl+c 可以結束程式並跳出
rl.on('close', function(){
    solve(lines)
})
//輸入結束，arr 裡面已經有輸入的資料，並執行 solve function
function solve(lines){
} 
//只要把解題方法寫在 solve function 裡面，要注意的是 function 裡面得資料是好幾列的 str ，要記得型別轉換才能處理

```

###### tags: `week3`