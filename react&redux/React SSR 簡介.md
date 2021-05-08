### Client Side Rendrering(CSR)
Server 會回傳 javaScript 而不是完整的 DOM 畫面，瀏覽器再利用 javaScript 重新取得資料，並在瀏覽器端重新整合畫面，不利 SEO

### Server Side Rendering(SSR)
瀏覽器直接回傳完整的畫面，瀏覽器直接 render，有利於 SEO


### react SSR 工具
- react DOM server
- renderToString()
``ReactDOMServer.renderToString(element)``
會把 react element render 回去原本的 HTML DOM 元件，在靜態的網站已經足以讓 serch engine 爬畫面。但不足之處是無法反應動態網站的動作如 onClick 事件等。
![](Pasted%20image%2020201210120437.png)

- hydrate()
``ReactDOM.hydrate(element, container[, callback])``
hydrate 可以幫助在 renderToString() 後在執行事件，保證 client 看到是動態的網站。
![](Pasted%20image%2020201210120855.png)

### SSR 框架
上面兩個 react 提供的 SSR 工具雖然堪用，但在有諸如 ``useEffect(fetch...)``等要 call api 才能取得完整資料的網頁，其實透過 ``hydratc()`` 是無法取得資料的，所以我們要透過某些輔助做 SSR 的框架來達成
### prerender.io
prerender 其實就是開了一個伺服器，先造訪網站並取得畫面資料後存起來，當之後 serch engine crawl 的時候回傳資料。

- 原理  
透過在 server 上安裝 prerender middleware，prerender middleware 會偵測該次訪問是否是 crawler，如果是 crawler 就會發 request 給 prerender 取得 HTML 靜態內容並回傳。

### Next.js
a React Framework，以 React 為 base 建立的框架，特色如下
- 內建 server side rendering
- 沒有 React-routing ，路由改由 ``pages`` 下面建立 ``.js`` 檔案，例如
``about.js`` 你就可以在 ``http:basepath/about`` 找到網頁，如果要做 SPA 或參數網址的話則用 dinamic routing 的方式，如``[id].js`` 的檔名
- prerender (SSG vs SSR)
  Next 是一套建構在 React 上的 SSR 框架(Vue 也有類似的框架 Nuxt)。
  Next 提供了兩種不同的 prerender 方式
  一個是 static generation(SSG)， static generation 會在 build 階段就預先渲染好 HTML，並在其後的每一個 request 使用同樣的 HTML，所以 SSG 比較適用於靜態網頁。
  另一種是 server-side Rendering，SSR 會在每一次 request 都重新預渲染 HTML。
  
#### static generation(SSG) 和相關 async funciton
- getStaticProps()
next 提供的 async function method，會在 build 階段請求 staticProps 並且利用 props prerender HTML
```js
function Blog({props}) {
	return (
		JSX...
	)
}

export async function getStaticProps(context) {
  const res = await fetch(`https://.../data`)
  const data = await res.json()

  if (!data) {
    return {
      notFound: true,
    }
  }

  return {
    props: {}, // will be passed to the page component as props
  }
}
```
getStaticProps() 也可以搭配 TypeScript 使用
```js
import { InferGetStaticPropsType } from 'next'

type Post = {
  author: string
  content: string
}

export const getStaticProps = async () => { ...
```
- getStaticPaths
如果有 dynamic routing 的話要 export getStaticPath ，這樣 next 就會在 build 階段把所有 path 的內容都先 prerender
getStaticPaths 要 return path / fallback 等參數
#### SSR 和相關 async funciton
在 next 9.3 之後， next 推薦使用 getServerSideProps 或 getStaticProps
- getServerSideProps
僅能運行在 server side
getServerSideProps() 會在每一次 request 都拿 props 並 pre-render
- getInitailProps
一開始會運行在 server side ，並預先拿取 props，後來就會在 client side 運作。
會接收單一 argument(pathname / query / asPath / req / res / err)
getInitailProps 提供一個位址，可以在 render 前先 call API 並拿回一個 stars 的值，這可以幫助我們輸入我們自己要的 url 並事先取得相關資料
注意 getInitialProps return 的必須是 serialize object
```js
About.getInitialProps = async() => {
	const res = await fetch("url")
	const json = await res.json()
	return {stars: json.stargazers_count}

}

```

#### CSS 
在 pages 資料夾底下放一個 _app.js file 裡面設定並 export function ，就可以達到類似 global style 的 效果
```js
import '../styles.css'

export default function MyApp({component, pageprops}) {
	return <Component {...pageProps}
}
```


### vercel 
搭配 next 部屬的框架