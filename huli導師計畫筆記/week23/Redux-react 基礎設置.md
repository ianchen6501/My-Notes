### React-redux / Redux Toolkit
目前 react 推薦使用更新的 Redux toolkit ，但因為還是常會見到 React-tedux ，所以還是先從 React-redux 入門。

### redux 設置
#### 建立 redux 資料夾
##### 建立 store.js
> 保存 store 的唯一方式，要改變 state 只能靠 dispatching，也可以搭配 subscribe 來連動 UI

> 不要建立超過一個 store，相反的可以透過 ``combineReducers`` 來創造一個 ``root reducer`` 接收不同 state 的 action

> state 盡量建立 plain object，並且修改 state 的時候應該用 ``object.assign({}, newstate)`` 或 {...state, ...newData} 的方式避免複寫原有的值

- createStore(reducer, [preloadedState], [enhancer])
初始化 store
``reducer`` a reducing function
``preloaded state`` initial state
``enhancr`` 搭配第三方功能如 middleware

- rootReducer
負責處理所有傳進 store 的 dispatch ，並決定 state 的狀態，在 store 裡面透過``createStore(rootReducer)`` 可以把 reducer 跟 store 串接起來，之後就可以透過發出 dispatch(action) 來更新 state

#### 在 redux 資料夾下面建立 reducers 資料夾
##### 在 reducers 資料夾，下面建立 index.js 
- combineReducer
combineReducer 可以整合不同的 reducer 成為一個物件並傳入 store。
``combineReducer({reducer1, reducer2})`` 

- reducer
一個 function ，會根據傳入的 action type 來決定回傳值，參數接收 ``initial state`` 及 ``action``
```js
const myReducer = (initialState, action) {
	switch(action.type) {
	case1 : 
		return ...
	case2 :
		return ...
	}
}
```

#### 在 redux 資料夾下面建立 actions.js
> 這比較像是幫助整理的輔助方法，這邊可以放不同的 dispatchs(actions)，actions 其實就是要藉由 ``dispatch`` 傳 value 進去，然後 reducer 在藉由 action type 來決定處理方式
```js
	const sampleAction =(value) => {
		return	{
			type : actionType,
			payload : {
				value
			}
		}
	}
```

#### 在 reudux 資料夾下面建立 actionTypes.js 
> 上面的 action type 其實我們可以另外再獨立出一個 actionTypes 的檔案來管理，裡面其實就是回傳 actionType name

``export const ADD_TODO = 'addTodo'``

### App.js 引入 selector / dispatch
> 在 app.js 裡面如果要拿取 store 裡面的 state 要透過 react- redux 提供的 hook ``useSelector``，而如果要使用 action 則要另外引入 dispatch 和 actions

#### useSelector
``useSelector(store => store.state.childstate)``

#### 建立 selectors.js
這時候我們也可以把 useSelector 的參數另外放到 selectors.js 管理
``const selectState = store => store.state.childstate``
那我們就可以把上面的 useSelector 改成
``useSeclector(selectState)``

#### useDispatch
在 app.js 拿 action 比較簡單，只要 import ``useDispatch`` 並 ``const dispatch() = useDispatch()`` 就可以用 ``dispatch`` 傳 function 進去 reducer 處理

### 在 index.js 引入 Provider / store
接著只要在 ``<App />`` 外面包上 ``<Provider store = {store} ></Provider>`` 就成功的把 Redux 引入 React 了

### Redux DevTool
#### 設置流程
1. 在 chrome extension 下載 redux-devtool-extension
2. 在 app 的 createStore 加上 enhancer 
```js
const createStore(rootReducer,
window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
)
```
#### 功能
action / diff / state / test

[redux_devtool](https://github.com/zalmoxisus/redux-devtools-extension)
[redus 中文入門](https://chentsulin.github.io/redux/docs/basics/ExampleTodoList.html)



