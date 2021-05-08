### 簡介
- 以 JavaScript 為基礎，但針對型別有特別定義的一種語言，可以幫助 vscode 等編譯軟體來判斷型別並給提示等，要要執行前還是要 compile 成 JavaScript。
- 檔案名稱 ``.ts``
舉一個 add function 為例子，TypeScript 要事先定義型別
```js
function add(a: number,b: number) {
    return a + b
}
```
我們甚至也可以設置一個 object 來規定型別
```js
interface UserProps {
	id: number,
	name?: string, //加問號表示非必須
	email?: string,
}

function logUser(user: UserProps) {
	console.log(user)
}

logUser({
	name: "huli"
})
```

### reference
[TypeScript](https://www.typescriptlang.org)

