# [第三周] - [JS102] - 利用 Jest 來寫你的第一個測試！
### Jest 簡介
- 一個用來執行"前端單元測試"的開源 module

### 環境設置
1. 在要安裝 jest 的資料夾用 terminal 執行下列指令，就可以把 jest 安裝下來。
> yarn add --dev jest 

or
> npm install --save-dev jest
2. 在資料夾建立兩個檔案。 
> 1. function.js 
> 2. function.test.js  (_.test.js是慣行寫法)
3. 接著在 function.js 裡面 export function
```javascript=
function sum(a, b) {
  return a + b;
}
module.exports = sum;
```
4.接著在 function.test.js 裡面寫要用 Jest test 的內容，注意一開始要先 require function.js ，接著用 test 指令來輸入要 test 的方式與預期結果。

```javascript=
const sum = require('./sum.js');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1,2)).toBe(3); 
})
//'adds 1 + 2 to equal 3'是對測試內容的描述
//expect 裡面要輸入的函式及變數
//toBe 輸入預期的結果
```
5. 接著要開啟 jest ，因為 jest module 不是 global ，所以在 terminal 裡面不能用 "node jest" 的方式來開啟，要打開 package.json ，並更改裡面的 "script" 來開啟，方式如下。
> "scripts": {
    "test": "jest"
    "test_sum": "jest sum.test.js" //只 test 單一檔案
  },
6. 接著在 termial 輸入下列指令
> npm run test
7. 最後會跑出測試的結果
![](https://i.imgur.com/6trF9aw.png)
8. 如果 npm 版本夠新也可以直接在 termial 用 npx 指令來執行
> npx jest function.test.js
9. 如果要寫多個 test 可以用一個 describe function 包裹
```javascript=
describe('測試 sum', () =>{
  test('adds 1 + 2 to equal 3', () => {
    expect(sum(1,2)).toBe(3); 
  })
  test('adds -1 + 1 to equal 0', () => {
    expect(sum(-1,1)).toBe(0); 
  })
  test('adds 100000 + 200000 to equal 300000', () => {
    expect(sum(100000,200000)).toBe(300000); 
  })
})

```
###### tags: `week3`