### 緣起
因為 Redux-React 被詬病有太多的前置作業(boilerplate)需要完成，所以在 Redux-Toolkit 裡面被整合起來。

### 基本環境建置
create-react-app
``npx create-react-app my-app --template redux``
exiting App
``npm install @reduxjs/toolkit``

### basic method
- configureStore 
加強版的 ``createStore``，透過 configureStore() 可以簡化設定的流程、結合 slice reducers、添加和 Redux 有關的 middleware、並啟用 Redux DevTools 的擴充套件。
```js
import {configureStore} from '@reduxjs/toolkit'
const store = configureStore({
	reducer: counter
})
```

- createAction
其實應該是 ``createActionCreator`` ，可以用來幫助節省設定 ActionTypes 的時間。
```js
// before
const ADD_TODO = "add_todo"
function addTodo() {
	return {
		type: ADD_TODO,
		...
	}
}
// after
const addTodo = createAction("add_todo")
console.log(addTodo)
// {type: "add_todo"}
```
如果要拿出 action 裡面的 string，則有兩種方法``.toString()``、``.type``
```js
console.log(addTodo.toString())
console.log(addTodo.type
// "add_todo"
```
createAction 產生出來的 creator 會自動包含 ``type``、``payload`` 等兩個參數，``payload`` 可以直接當作參數帶進去 creator
```js
const increment = createAction("INCREMENT")
increment()
//{type: "INCREMENT", payload: undefined}
increment(5)
//{type: "INCREMENT", payload: 5}
```

- createReducer
createReducer() 這個工具提供你一張 action type 和 reducer 的對應表，而不用使用 switch 語法，此外它自動使用 immer library 這個工具，讓你可以使用「immutable」的方式來變更資料狀態，例如，state.todos[3].completed = true。
```js
const increment = createAction("increment")
const decrement = createAction("decrement")

const counter = createReducer(0, {
	[increment.type]: (state, action) => state + 1,
	[decrement.type]: (state, action) => state - 1,
})
// 也可以改成
const counter = createReducer(0, {
	[increment]: (state, action) => state + 1,
	[decrement]: (state, action) => state - 1,
})

```

- createSlice
createSlice 可以達到在同時設定 reducer、creator。在 createSlice 可以帶入 slice name、initialState、reducers ，並產生對應 reducers、action creator

```js
const counterSlice = createSlice({
	name: "counter",
	initialState: 0,
	reducers: {
		increment: state => state + 1,
		decrement: state => state - 1,
	}
})

const store = configureStore({
	reducer: counterSlice.reducer
})
```
同時我們可以用解構語法來拿到其中的 actions
```js
const {actions, reducers} = counterSlice
const {increment, decrement} = actions
```
總結我們可以透過 counterSlice 拿到下列資訊
```js
// slice name
counterSlice.name //counter
// reducer
counterSlice.reduer
// action
counterSlice.actions.increment()
counterSlice.actions.decrement()
// actionType
counterSlice.actions.increment.type
counterSlice.actions.decrement.type
```

- reference
[[Redux] Redux Toolkit(RTK) 筆記](https://pjchender.github.io/2019/02/15/redux-redux-toolkit-rtk-筆記/)
