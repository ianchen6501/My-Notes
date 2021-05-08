

### 強烈建議
1. 不要直接操作 State
2. Reducers 絕不可以有副作用 (Side Effects)
不可以在此進行任何非同步的行為(像是呼叫 AJAX, timeouts, promises)，也不可產生隨機的值(Date.now(), Math.random())。若想這麼做，請在 reducer 外面設置變數或是在 reducer 的 scope 外面做。
3. 別將不可序列化的值放在 State 或 Action 裡
請避免將不可序列化的值（例如 Promises、Symbols、Maps / Set、function 或 class 的實例）放入 Redux store state 或 action 裡。

### 次級強烈建議
1. 使用 Redux Toolkit 來撰寫 Redux 程式碼
2. 使用 Immer 來撰寫 Immutable 的 state 更新
3. 以功能性分類或 「Ducks」模式來作為檔案結構
4. 盡量將程式邏輯寫在 Reducers 裡(當然要寫在 dispatch 也不是不行，只是會難以測試維護)
5. State 的形狀應由 Reducer 來決定
每個 reducer 負責提供一個初始的 state 並且負責計算與更新對應的新 state。
6. 用 State 內儲存的資料來決定 State 的名稱，並避免帶有 ``reducer`` 字眼的 key 名稱
```js
combineReducers(
	{
	todos : todosReducer,
	users : usersReducer
	}
)
```
7. 將 Reducers 當作是狀態機
我們能將 reducers 當作是一個 “狀態機”。這個狀態機能夠結合目前的 state 與被 dispatch 的 action 來計算新的 state
8. 將 Action 以事件的方式建構，而不是 “Setter”
```js
{
	type : "pizza/orderAdd",
	payload : {
		pizza : 1
	}
}
```
會比下面的好
```js
{
	type : "setPizzaAmount",
	payload : {
		amount : getState().pizza.amount + 1 
	}
}
```
8. 避免連續 dispatch 多個 action
9. 衡量每個 State 到底該存在哪裡
10. 將你更多 component 都連結上 store 來讀取資料
11. 在 Function Components 內多次使用 useSelector ，並一次只取用需要的資料

### ㄧ般建議
1. 將 Action Types 寫成 domain/eventName 的格式
2. 以 “Flux Standard Actions” 的原則撰寫 Action
> - 應將資料放進名為 payload 的欄位
> - 能有一個名為 meta 的欄位來提供額外資訊
> - 能有一個名為 error 的欄位來回報錯誤
3. 使用 Action Creator 或 Redux ToolKit 的 createSlice

[Redux Style Guide](https://medium.com/@a401120174/tr-85e00315cd73)