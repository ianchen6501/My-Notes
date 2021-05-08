### 緣起
- Redux thunk 是一個 Redux middleware
- 傳統的 action 是一個 pure JavaScript Object，但當我們想在 dispatch 前做某些處理再正式發送時，就可以透過 Redux thunk 這個 middleware，他會幫助我們在事前處理(setimeout / ajax ...) 完成後再執行 dispatch
![](Pasted%20image%2020201203135954.png)

### 基本用法
```js
function incrementAsync(amount) {
	return function(dispatch) {
		setTimeout(() => {
			dispatch(incrementByAmount)
		}, 1000)
	}
}
// 一秒後發出 dispatch(incrementByAmount)
```

### reference

[[Redux] Thunk](https://pjchender.github.io/2018/09/13/redux-thunk/)