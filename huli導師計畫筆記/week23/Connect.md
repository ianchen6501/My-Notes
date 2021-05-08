### 簡介
ㄧ般來說我們只要透過 ``<div onClick={dispatch(action(state))} />`` 就可以達到目的。但 hooks 出現前就要倚靠 ``connect``

### connect method
- connect
使 react 取得 redux 中的 state
``function connect(mapStateToProps?, mapDispatchToProps?, mergeProps?, options?)``

- mapStatetoProps
當 redux store 有變動的時候，react component 可以訂閱到這個變動
必須回傳一個物件，或回傳 null(如果你不希望訂閱 store，變動)
state 也可以拿來當 selector 使用，指定要輸入當 props 的物件
```js
const mapStateToProps = (state, [ownProps]) {
	return {
	}
}
```

- mapDispatchToProps
一個物件 或 function，或兩者都不是
```js
mapDispatchToProps(dispatch, [ownProps]) => {
	return {
		dispatchprops...
	}
} 
```

- bindActionCreators
```js
bindActionCreators
```





[Redux - connect](https://react-redux.js.org/api/connect)