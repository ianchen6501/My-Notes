### 基礎
`new Date()` 建立一個 Date 物件，裡面會有許多 method 可以使用
`Date.now()` 回傳1970年到目前的時間的毫秒數
`Date.getHours()` 回傳當地的小時

### 計數器
```js
const [time, setTime] = useState(null)

setTimeout(() => {
	const Hours = Date.getHours()
	const Minutes = Date.getMinutes()
	const seconds = Date.getSeconds()
}, 1000)

return <time>time</ time>
```