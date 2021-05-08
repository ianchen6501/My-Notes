# Webpack
### module bundler
> 可以執行像 gulp 一樣的打包動作，並在瀏覽器上執行。
原因應該是因為原本在 node.js 上我們可以用 module.export + require 來引入或輸出 module ，但在瀏覽器上不行，儘管現在新的瀏覽器可以用 export / inport 等指令來達成，但為了適用性，webpack 還是很需要
### 環境建置
> 一樣安裝``npm install --save-dev webpack``，然後素材檔案放在 ``src`` 輸出後會放在 ``dist``，並且可以透過 webpack.config.js 裡面來設定***輸出檔案***、***路徑***、***模式***等等，模式包含(development/production)

### index.js
在這裡面我們可以 require 不同的檔案如 jquery/ui.js/utils.js 等等，然後有 require 的才會進行 bundle

### webpack plugin / loader
[請參考這篇文章](https://neighborhood999.github.io/webpack-tutorial-gitbook/Part1/IntroductionPlugin.html)
可以在 loader 加入 babel、sass等處裡

### webpack devServer
可以 livetime 的 renew 變更，使用方式是先下載 devServer 後，在 package.json 設定 strat ，接著用 ``npm run start`` 的方式就可以開啟，要注意的是 index.html 的檔案要放在 dist 資料夾，server 才可以開啟模擬。 
- 關閉用 ctrl + c

### devServer Sourcemap 
幫助在 devtool 直接觀察打包後的原始 code

### HtmlWebpackPlugin
可以在 html 為空的狀態下，由 webpack 利用 js 產生一個 html 檔

### template 
用來設定上面 html 的 template 檔


###### tags: `week13` `webpack`