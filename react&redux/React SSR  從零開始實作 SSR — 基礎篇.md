### 時間軸
CSR、SSR 請求及在畫面上呈現的時間不同。SSR 伺服器會直接回傳 HTML DOM 畫面，但 CSR 則必須再另外透過請求 JS、Mount React 物件、call API 拿資料、監聽等動作才可以拿到最終 HTML 畫面。
![](Pasted%20image%2020201210165154.png)

### SEO / UX 差異
除了 google 外，其他的搜尋引擎並不會另外做 JS 請求及 React mount 、call API 等動作，這會造成 SSR 及 CSR 在 SEO 效果的差異，SSR 因為網頁在 server 端就處理好了，所以可以爬到完整的 HTML 內容。同時也可以縮短使用者看到完整畫面的時間，有助於 UX。

### React 的 SSR 原理
React SSR 的原理是透過一個渲染伺服器來達成，渲染伺服器的功用在於使用者第一次請求 HTML 的時候會跟後端拿資料並放入 HTML 裡面，所以使用者可以看到完整的網頁。
React SSR 的特性如下:
- 擁有一個獨立的伺服器 (後端)，提供 API 可以請求資料。
- 渲染伺服器與瀏覽器端都可以請求 API。
- 渲染伺服器會在使用者請求 HTML 時，會請求 API 的資料，並將內容都事先放到 HTML 中。
- 在第一次請求 HTML 後，之後的元件 routing、請求 API 都是在瀏覽器端執行。
![](Pasted%20image%2020201211102551.png)

### 實作_基本環境建置
- 安裝 express / webpack / babel / nodemon
express 用來作為渲染伺服器使用，webpack / babel 則是要打包 client / server 兩個檔案，nodemon 則是作為自動化工具使用

### 實作_basic SSR
我們可以透過 react 提供的 .renderToString() 功能來取得靜態的 HTML DOM 元件。官方文件說 renderToString() 方法可以將 React element render 成原始的 HTML，並在伺服器端回傳。

伺服器端的實作則可以透過 Express 來達成，簡易的 API 如下。
```js
const app = express()

app.get("/", (req, res) => {
	const content =  renderToString(<Home />)
	res.send(content)
})
```

但這樣子透過 express 拿回來的 HTML 資料並不包含監聽等動態 JavaScript 行為，所以要再透過其他方法來確保使用者可以看到正確的畫面。

### .hydrate() 注入
在獲得初始 HTML 資料後，為了確保 JavaScript 動態事件正確執行並顯示到螢幕上，React 提供 hydrate 功能來綁定事件。

- client.js
我們另外建立一個 client.js，裡面用來設定 hydrate
```js
ReactDOM.hydrate(<Home />, document.getElementById('root'))

```

![](Pasted%20image%2020201210173326.png)

### reference
[React SSR | 從零開始實作 SSR — 基礎篇](https://medium.com/手寫筆記/server-side-rendering-ssr-in-reactjs-part1-d2a11890abfc)