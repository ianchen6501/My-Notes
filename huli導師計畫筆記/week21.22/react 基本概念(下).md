### react 的渲染機制
- Virtual DOM
可以看作是一個 React 產生的虛擬節點
```js
{
tag: 'div',
props: {
	className: 'App'
}
children: {
	...
}
}
```
react 會透過比對變更前後的 virtual DOM 來確定哪些部分需要 re-render

### 渲染性能優化
react 當 props 或是 state 有改變的時候，都會 re-render ，但其實有時候 child conponent 其實不需要 re-render ，因為 UI 其實沒有變動，這時候就可以透過設定 memo / useCallback / useMemo 等來優化
- memo()
其實就是 shallow equal 比對(pureComponent)，用法是包在 component 外面
``memo(component)``
props 沒有改變的時候，就不會 re-render，但如果 props 是 object 因為記憶體位置會改變，還是會造成 re-rerender
- useCallback
 > 當 props 是一個callback function 時，React.memo 需要搭配 useCallback 使用。
```js
const memorizeCallbacks = useCallbacks(() => {
	dosomething(a, b)
}, [a, b])
```
因為 callbacks 是一個 function，每次執行時都會有不同的記憶體位置，
透過設定 dependency array 的方式，react 會幫我們記住記憶體位置，判斷 object 值不變的話，就不會重新賦予記憶體位址。
ㄧ般來說 useCallback 會加在 callBack 前面，並搭配 React.memo 使用
``useCallback(fn, deps) 相等於 useMemo(() => fn, deps)。``
- useMemo
> 當我們希望 React 幫我們記住某些 props 或 state 當他們改變的時候才 rerender
```js
useMemo(() => {
  return somthing
}, [a, b])
```



[React 性能優化那件大事，使用 memo、useCallback、useMemo](https://medium.com/手寫筆記/react-optimize-performance-using-memo-usecallback-usememo-a76b6b272df3)
[關於props的記憶，React Memo (新增範例及說明)](https://ithelp.ithome.com.tw/articles/10240296?sc=iThomeR)

### React 的事件機制
當我們在 child component 掛事件時(onChange, onClick...)，其實是在 root 監聽，然後再用事件代理的方式來處理。

### class component


### prop drillling / useContext & createContext
當有多層的 component 架構的時候，props 要一層一層傳下去，就是 prop drilling 的概念。為了要解決這個問題需要透過 useContext。
所以存在 context 裡面的資料其實有 global 全域的概念。
1. ``import {useContext, createContext} from 'react'``
2. ``const Context = createContext()`` 初始化 context 並傳入初始值
3. 接著在要使用 Context 的地方外面包住 ``<Context.provider value={props}`` value 裡面放 props
4. 並在要使用 props 的地方 ``const props = useContext(Context)``

[I Want To Know React - Lifecycle 階段](https://ithelp.ithome.com.tw/articles/10244959)

### 增進程式碼品質
- vsCode - eslint extension
- proptypes - check the props type is correct or not 
用途是在 component 裡面設定 props 的型別，方法是透過 react 內建的 PropsType
```js
component.PropsTypes = {
	name: propsTypes.string
}
```
設置流程:
1. 新建一個 .eslintrc.json ，裡面[重新設定](https://create-react-app.dev/docs/setting-up-your-editor/)
```js
{
  "extends" : ["react-app"],
  "rules": {
    "react/prop-types" : "warn"
  }
}
```

### react router
- BrowserRouter 網址會以 ``site/...`` 來呈現，在 githubpage 這樣會噴錯，因為 githubpages 是直接去檔案裏面找，但在 router 中是透過 JavaScript 去執行
#### 基本元件
1. BrowserRouter / HashRouter
BrowserRouter 換頁面會發送 request 重新渲染，路徑會像是這種型式``/site/childsite``
HashRouter 換頁面不會發送 request 也不會重新渲染，路徑會像是這種型式``/site/#/childsite``
使用 Router 的時候要用 ``<Router>`` tag 把要做頁面轉換的地方包起來
2. Route
Route 用來設定頁面，位置要放在 ``<Router>`` 中，``<Route path={'/'} component={`頁面名稱`}``，Route 裡面就可以放要引入的內容(通常是一個外部引入的 component)
3. Switch
通常 Route 外面會用 ``<Switch>`` 包起來，Switch 可以判斷要去的位址並只渲染其中一個 Route。
4. Link
當要實際做路徑時，可以透過 ``style.(Link) `` 或 ``<Link>`` 或 來做一個等同於連結物件，Link 裡面要放 ``path={'/pathname}`` 來指定位址

#### hook
- useHistory
通常用來導向某個頁面(如前頁)
``imsport {useHistory} from react-router-dom``
``const history = useHistory()``
``history.push('/')``

[【React.js入門 - 27】 我要更多更多的分頁 - react-router-dom (上)](https://ithelp.ithome.com.tw/articles/10226056)
[react router](https://reactrouter.com/web/guides/quick-start)

### 登入 / 身分驗證
#### ㄧ般的身分驗證
![](Pasted%20image%2020201121094446.png)
#### react 的身分驗證
![](Pasted%20image%2020201121094648.png)
這邊是用到 JWT(JSON Web Token)來做身分驗證，JWT 會傳送一個包含 Header / Playload / Verify Signature 的 JSON 檔案，注意因為 JWT 是用 base64 轉碼，還是可以透過 decode 來解析，所以裡面不要存重要的個資

[huli-student-api-login](https://student-json-api.lidemy.me/login)
{"username":"user01", "password":"Lidemy"}
[huli-student-api-me](https://student-json-api.lidemy.me/me)
這邊帶 token 進去就會回復使用者資訊

### link
[blog](https://ianchen6501.github.io/w22-react-blog/)


