### 淺談狀態管理
ㄧ般(Jquery): 資料與畫面是分開的
react : 只要管資料，react 會自動 render 畫面
angular / vue : 資料與 UI 雙向綁定 

> 不一定所有的資料都要存在 redux，通常只有一些 global 的資料(如帳號狀態)，不想要一直透過 props 傳遞，才會存在 redux


### flux
- flux 一開始是為了解決複雜專案的狀態管理應運而生的工具，所以如果今天專案規模不需要，用 flux 或許無法解決問題。
- flux 把資料處理多了一個 dispatcher 的概念，當使用者從 view 發出指令(action)的時候，會傳到 dispatcher 分發處理，才會進到 store 去處理資料。

### redux 簡介
- react useReducer : useReducer 與 flux 的狀態處理方式很相像，也是透過 dispatch 設定處理方法，然後把狀態存到 state，reduce 則是設定一個處理方法的函式。

![](https://static.bookstack.cn/projects/reactjs101-zh-tw/Ch07/images/redux-flowchart.png)

傳統的 mvc 架構資訊流
![](https://miro.medium.com/max/875/1*y80ch5iiHve09zM7SpTlkA.png)

flux unidirectional flow
![](https://miro.medium.com/max/875/1*pgxTL69KXTYjupzGO015Ew.png)


### Redux 簡介
- installation 
``npm install @reduxjs/toolkit``
``npm install redux``
- 創建一個 react-redux app ``npx create-react-app my-app --template redux``

接著我們可以透過一個簡單的 example 來學習 redux
```js
function counterReducer(state = { value: 0 }, action) {
  switch (action.type) {
    case 'counter/incremented':
      return { value: state.value + 1 }
    case 'counter/decremented':
      return { value: state.value - 1 }
    default:
      return state
  }
}

let store = createStore(counterReducer)

store.subscribe(() => console.log(store.getState()))

store.dispatch({ type: 'counter/incremented' })
```
在 redux 裡面，我們沒辦法直接去改變 state ，而是要透過發出 action 並經過 reducer 處理過後才會更改到 state
> Instead of mutating the state directly, you specify the mutations you want to happen with plain objects called actions. Then you write a special function called a reducer to decide how every action transforms the entire application's state.

同上面可以注意到用 switch 來取代 if / else 判斷，是為了因應當 dispatch type 變多的情形。下面是一個基本的 switch case
```js
const expr = 'Papayas';
switch (expr) {
  case 'Oranges':
    console.log('Oranges are $0.59 a pound.');
    break;
  case 'Mangoes':
  case 'Papayas':
    console.log('Mangoes and papayas are $2.79 a pound.');
    // expected output: "Mangoes and papayas are $2.79 a pound."
    break;
  default:
    console.log(`Sorry, we are out of ${expr}.`);
}
```

### Store method
- getState
- subscribe
- dispatch

### store 基本操作
- set ActionTypes
當 dispatch(action) 數量增加的時候，要先設定 Action Constants 然後在之後的 dispatch 引用，這樣才可以避免打錯找 bug 的麻煩，另外如果沒有設定 actionConstents 系統不會報錯，因為他就只是一個沒有設定的 action type，例如
```js
const ActionTypes = {
  ADD_TODO : 'add_todo',
  DELETE_TODO : 'delete_todo'
}
```
- set Action Creator
當我們 action 的數量變多的時候，要一直重複寫同樣的 action 內容會很麻煩，所以透過一個 function return action ，可以精簡程式碼，這就是 action creator 的功能。
```js

```
- create reducer
```js
function AppReducer(initialstate, action) {
	switch() {...}
}
```
- create store
``let store = createStore(reducer)``
- store method
``store.subscribe(() => {...})``

*這邊要注意更新 state 的時候要寫*
```js
return 
{...state, [newState]}
```
*不然如果 state 裡面有多個 item ，其他沒有更新的會被覆蓋掉*
*另外 reducer 要是 pure function 的形式，裡面不可以有 call api、setLocalStorage 等行為*
*payload 就是一個參數的命名慣例，通常用在 API carry 的 核心資料，如*
```js
	{	ok: true
		message: 'hello world'
	}
```
*上面的 hello word 就是 pay;oad*

reference: 
[Redux 基礎概念](https://www.bookstack.cn/read/reactjs101-zh-tw/Ch07-react-redux-introduction.md)
[[實作]使用 Redux 實作 Todo-List](https://medium.com/lion-f2e/實作-使用-redux-實作-todo-list-43fd1d73d4c1)