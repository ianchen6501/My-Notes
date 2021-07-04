
### NPM
主要用在套件管理、下載，沒辦法直接執行 module ，如果要執行 module，要先在 package.json 設定 script 例如
```js
{
  "name": "whatever",
  "version": "1.0.0",
  "scripts": {
    "some-package": "some-package"
  }
}
```
接著輸入
``npm run some-package``

### NPX
npx  會自動偵測 local 跟 global 有沒有安裝 module ，並透過 ``npx come-package`` 來運行，他還有另外一個好處是可以在不安裝 module 的情況下 create 一個新的 app ，並在結束執行後自動刪除，不會汙染全域環境 ``npx create-react-app my-app``


### reference
[Difference between npx and npm?](https://stackoverflow.com/questions/50605219/difference-between-npx-and-npm)