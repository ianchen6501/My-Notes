### 測試種類
unitest / integration test / end to end test

### react testing library
unitest
[react-testing-library](https://testing-library.com/docs/react-testing-library/intro/)

### cypress
- 初始化建置
為一種 end to end test
``npm install cypress --save-dev``下載 cypress
``npx cypress open`` 在資料夾做 cypress 初始化，cypress 會在母資料夾下初始化測試的檔案
修改 cypress.json 增加 ``"baseUrl": "http://localhost:8080"``
在 integration 資料夾新增 ``sample_spec.js`` 裡面可以書寫測試內容如
```js
describe('The Home Page', () => {
  it('successfully loads', () => {
    cy.visit('/')
  }) 
})
```
接著在 open cypress 裡面啟動 sample_spec.js cypress 就會開始測試了

- mock :
要使用到 cypress 的 cy.route / cy.intercept API
並在 spec.js 增加如下列 route method
```js
    cy.server()
    cy.route('https://student-json-api.lidemy.me/posts', {
      id : 1,
      title: 'sss',
      body: 'aaa'
```
cypress.js 要一併增加 flag
```js
"experimentalFetchPolyfill": true
```


*使用 pm2 run react-create-app ``pm2 start my-app/node_modules/react-scripts/scripts/start.js --name "my-app"``
 

[cypress](https://www.cypress.io)