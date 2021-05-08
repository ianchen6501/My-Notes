### replace(stringA, stringB)
更改字串內容，注意只會更改第一個符合的字串，要全部取代要用正規表達式

```js
const string = "mother"
console.log(string.replace("th", "ch")) //mocher 

const string = "yo,yo,yo"
console.log(string.replace("/,/g", "")) //yoyoyo
```