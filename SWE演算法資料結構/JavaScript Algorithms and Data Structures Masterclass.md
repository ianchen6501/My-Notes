### Intro to big O
- time complexity / space complexity
- to have a precise vocabulary to talk about how our code perform
- to discuss trades-offs between different approaches
- to identifying parts of the code that are inefficient

### what does better mean
回過頭來先看一下怎麼來評斷好的程式碼
- faster
- less memory-intensive
- more readable

### 如何去描述 big(O)
- 不論 n 為何值，執行的次數都是常數 -> O(1)
- 執行的次數跟 n 成等比 -> O(n)
- 執行的次數跟 n 平方成等比 -> O(n2)

### 來看一些例子
```js
function addUp(n) {
	return n*(n+1)/2
}
//O(1)
```

```js
function addUp(n) {
	let total = 0
	for(let i=0; i<=n; i++) {
		total += i
	}
	return total
}
//必須要加 n 次，所以big O = O(n)
```

```js
function countUpAndDown(n) {
	console.log("going up")
	for(let i=0; i<=n; i++) {
		console.log(i)
	}
	console.log("going down")
	for(let j=n; i>=0; j--) {
		console.log(j)
	}
	console.log("bye")
}
//O(2n) --> O(n)
```

```js
function printAllPairs(n) {
	for(let i=0; i<n; i++) {
		for(let v=0; v<n; v++) {
			console.log(i, v)
		}
	}
}
//O(n2)
```