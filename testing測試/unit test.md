## 定義
針對 function / method 驗證輸入、輸出的測試方法。
分為 TDD(Test-Deriven Development) / BDD(Behavior-Deriven Development) 兩種

## TDD
先寫測試程式，再實作功能。  
TDD 三定律：  
(1) 沒有測試之前不要寫任何功能代碼  
(2) 只編寫恰好能夠體現一個失敗情況的測試代碼  
(3) 只編寫恰好能通過測試的功能代碼

## BDD
使用 describe() 和 it()  
需求為導向的設計  
語意化

## JEST
### download
`npm install jest -D -S`
### 簡易測試
```js
const { expect } = require("@jest/globals")
const time = require("./time")

test("3 time 4 equal 12", () => {
  expect(time(3,4)).toBe(12)
})

```

### 在 React 裡面用 jest 測試
#### 測試步驟
1. 首先，要定義一下應該要測試什麼？ 例如「一個正常的按鈕」，表示「當按鈕被點擊時，他應該觸發相關函式」
2. 將組建引入，並且渲染組建：要先渲染出來，才能方便在後面抓取。
3. 利用選擇器抓取元素（要以渲染結果的樣子去思考）
4. 模擬使用者的動作，例如：點擊事件
5. 測試一下預期的結果是否發生

#### 常見的抓取器
getByText
getByLabelText
getByDisplayValue
getBytitle

#### 常見的模擬行為


### REFER
[Jest | 讓 Jest 為你的 Code 做測試-基礎用法教學](https://medium.com/enjoy-life-enjoy-coding/讓-jest-為你的-code-做單元測試-基礎用法教學-d898f11d9a23)
[初探 Test 與測試框架的選擇](https://medium.com/@envive.tw/前言-暴走gandhi-不知道大家有沒有玩過一款遊戲叫做-civilization-文明帝國-441891b116d7)
[給初學者的前端 Unit test 教學—— 以 React Testing Library 為例](https://nissentech.org/react-testing-library/)