### 環境建置
在要執行 react 的資料夾，cmd 輸入 ``npx create-react-app my-app``，接著就會建立 my-app 資料夾，然後輸入 ``npm run start `` 開始運行，ctrl + c 跳出

### component
為了讓網頁的元素可以重複複製、更新及調整，我們可以把它變成一個 component。
> Component 使你可以將 UI 拆分成獨立且可複用的程式碼，並且專注於各別程式碼的思考。

### 畫面(UI)與資料(data)
- 網頁呈現的內容其實包含畫面(UI)與資料(data)
- 當我們在資料庫儲存時其實是資料
![](Pasted%20image%2020201102191722.png)
- 要隨時確保畫面與資料一致，所以方法有兩種，一種是畫面改變時，資料從畫面的取得。另一種是資料改變時，畫面取得資料。
![](Pasted%20image%2020201102191826.png)

### JSX 
- ``const element = <h1>你好，世界！</h1>;`` 這個語法就是 JSX，意思是 react 可以直接輸入 html tag 再透過底層的 JS 去產生。
- JSX 可以帶入變數，要用 ``{}`` 包住
- JSX 物件可以做 JavaScript 運算
```js
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}

```
- JSX 可以防範 XSS，如果執意要讓 XSS working 的話要加上 [dangerslySetInnerHTML](https://zh-hant.reactjs.org/docs/dom-elements.html)，但針對 HTML 連結的物件如果在 href 裡面做 XSS 的話(click-base XSS)需要特別做處理，處理的方法是前面加上 ``window.encodeURIcomponent()`` 做完編碼後再輸出
- JSX 背後其實是用 ``React.createElement`` 來創造 element
- react element 更接近 JavaScript 所以命名要採 ``camelCase``
- 注意 JSX 運算沒有迴圈(for)跟條件(if/else)
- 另外如果想要 DOM tag 裡面的結構不想顯示某些變數的話，可以在前面加上 $ ，例如 ``$id = "id"`` 這樣 devtool 裡面就會看不到該 id，所以習慣上可以在傳給 styled component 的元素前面加上 $

### Render Element
- ``const element = <h1>Hello, world</h1>;``
- element 是 immutable

### component 
#### function component 
```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
- React 會將小寫字母開頭的組件視為原始 DOM 標籤，舉例來說，<div /> 就會被視為是 HTML 的 div 標籤，但是 <Welcome /> 則是一個 component
- 我們建議從 component 的角度為 props 命名，而不是它的使用情境。
- componebt 可以被組合和拆解
```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

#### class component
```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### component Array 的 key 值
當我們在映射 data array 成為 component array 的時候，如果沒有指定每個 component 的 key 值的時候，系統會通知要設定 key 值，如果沒有設定就會自動排序。而設定 key 值建議是用``資料唯一的值``當作 key (在 array 裡面不會有重複)，避免在 component 有新增刪除時，造成錯誤(如以 id 當作 key 值，刪掉其中一個後面會遞補)。所以總結來說 react 15 以後的行為如下:
- React在實際修改DOM之前，會比較前一次render跟目前這一次render結果的“差異”，同一個層級中的所有Component
- 若出現key值一樣但props不一樣的Component則進行更新
- 若比對所有key值後，發現有之前不存在的key值，則新增
- 若比對所有key值後，發現有之前存在的key值消失，則刪除
[重新了解React中的key (Part 1)
](https://medium.com/@mengweichen/重新了解react中的key-part-1-b211f8e88527)

### 嚴格模式
嚴格模式是一個用來突顯應用程式裡潛在問題的工具。
嚴格模式目前可以幫助：
> 發現擁有不安全生命週期的 component
警告使用了 legacy string ref API
警告使用到了被棄用的 findDOMNode
偵測意想不到的副作用
偵測 legacy context API

### props
夾在 JSX element 中間的值也是一種 props ，可以在 children element 中用 {children} 呼叫``<Div>children</Div>``


### style
1. inline style
要用 component 的方式建立，注意屬性因為是用 JSX 所以命名要採用 lower camel case。
另外 inline style 不支援 tsudo element / hover 等
2. css
- 可以在 component html tag 裡面加上 className(注意 class 在 JSX 是保留字，所以要改成 className)，並在 style.css 裡面更改。
3. [styled-component](https://styled-components.com)
- ``npm install --save styled-components``

### state
Local state
- 生命週期: component 更新的時間範圍
> 每當 Clock render 到 DOM 的時候，我們想要設定一個 timer。在 React 中稱為「mount」。
每當產生的 Clock DOM 被移除時，我們想要清除 timer。在 React 中稱為「unmount」。

- 生命週期方法:
``componentDidMount()``
``componentWillUnmount()``
``setState()``

- state 的更新可能是是非同步的

- 正確的使用 setState
請不要直接修改 State ``this.setStete.comment = 'hello'``
請改成 ``this.setState({comment: 'hello'})``

- State 的更新將會被 Merge，可以只更新其中一個 state 

### class component life cycle
![React Component 規格與生命週期](https://github.com/kdchang/reactjs101/raw/master/Ch04/images/react-lifecycle.png)
![React 生命週期(完整)](https://www.fooish.com/reactjs/component-lifecycle.html#shouldComponentUpdate)

### hook
- function component 因為不能使用 this.state ，所以在 16.8 版以後更新為使用 hook，就是可以用 ``const [state, useState] = ""`` 來設定 state(""為初始值)。注意一開始要 ``import {useState} from "react"``
- ``ref``用法是 ``import {useRef} from "react"``、``const inputRef = useRef`` 與 state 的差異是，當 ref 改變的時候不會 re-render
- hook 要注意不能放在 if/else 或 for 等語句中，react 會不給過(猜是因為 side effect

[React-hook](https://zh-hant.reactjs.org/docs/hooks-state.html)
[hooks api references](https://reactjs.org/docs/hooks-reference.html#useref)
[How Are Function Components Different from Classes?](https://iqkui.com/how-are-function-components-different-from-classes/)

### useEffect
- render 完，瀏覽器 paint 以後你想做什麼。在每一次 re-render 時都會在執行一次。
- 用法是 ``useEffect(() => {...})``，裡面可以做在下一次 render 前要執行的任務(存 state、localstorage ...)
- 裡面在 return 一個 arrow function 會變成一個 clean-up function ，clean-up function 會在下次 re-render 的 effect 執行前動作，所以裡面的 state 會是前次的值。主要用途就是在清除前次遺留的資料，或者是在 component unmount 時把 effect 清掉。

- 參考文章
[A Complete Guide to useEffect](https://iqkui.com/a-complete-guide-to-useeffect/)

### useLayoutEffect
- render 完，瀏覽器 paint 以前想做什麼
- hook flow diagram
![](Pasted%20image%2020201106132258.png)

### custom hooks
- 要新建一個 ``use`` 開頭的 js 檔案，裡面 export use... function
- 裡面可以 useState、useEffect 等動作，最後在 ``module default export {}`` 把函式變數等輸出給 app 用，這樣就可以達到 app 裡面只做 UI 的效果。

### 效果最佳化
- pure component
- 如果 component 沒有 state ，採用 function component 會更好

### 部屬到 github page(靜態)
* create a github repo
``npm run build`` build production locally
``npm install -g serve`` 建立 port 5000 server
``serve -s build``
revise package.json
```js
	"homepage": "https://ianchen6501.github.io/my-app",
	"scripts": {
	...
	"predeploy": "npm run build",
	"deploy": "gh-pages -d build"
	},
```
``npm install --save gh-pages`` install gh-pages
``npm run deploy``
set github-pages on github settings

如果在部屬上去後有問題的話，可以查看 /build/index.html 裡面 引用的 filepath 是否正確。

### 用 react 思考
- 第一步：將 UI 拆解成 component 層級
- 第二步：在 React 中建立一個靜態版本
如果是大型專案，由下往上一步一步測試會比較順利
如果是中小型專案，可以由上往下建構
注意，因為是靜態的版本，請不要使用到任何的 state
- 第三步：找出最少（但完整）的 UI State 的代表
這個資料是從 parent 透過 props 傳下來的嗎？如果是的話，那它很可能不是 state。
這個資料是否一直保持不變呢？如果是的話，那它很可能不是 state。
你是否可以根據你的 component 中其他的 state 或 prop 來計算這個資料呢？如果是的話，那它一定不是 state。
- 第四步：找出你的 State 應該在哪裡
找出使用者的共同擁有者 component
- 第五步：加入相反的資料流
建立可以在底層元件改變時可以更新 state 的機制

### control component / uncotrol component
- control component 
input / textarea / select / checkbox 等的值(value)可以透過 state 來綁定，當值變化的時候，state 也一起變化，這樣的物件就叫 control component。
可以先來看一個簡單的 form
```js
class EasyForm extends React.Component {
	render()
		return (
			<form>
				<label> 姓名: </label>
				<input id="name" name="name">
				<br/>
					<input type="submit" value="送出表單" />
			</form>
		)
}
```
當把 form 與 state 綁定，可以透過 ``<input value={this.state} onChange={this.changeState}`` 的方式
```js
class EasyForm extends React.Component {
	constructor(props) {
		super(props)
		this.state = {name : ""}
		//綁定 function this
		this.changeState = this.changeState.bind(this)
	}
	
	changeState(event) {
		this.setState({name: event.target.value})
	}

	render()
		return (
			<form>
				<label> 姓名: </label>
				<input id="name" name="name"
					value={this.state.name}
					onChange={this.changeState}
				>
				<br/>
					<input type="submit" value="送出表單" />
			</form>
		)
}
```


- uncontrol component


### practice_url
[todo-list](https://ianchen6501.github.io/w21-react-todolist/)
[gobang](https://ianchen6501.github.io/w21-gobang/)
[form](https://ianchen6501.github.io/w21-react-form/)

### reference
[The Lifecycle of React Hooks Component](https://blog.bhanuteja.dev/the-lifecycle-of-react-hooks-component)
