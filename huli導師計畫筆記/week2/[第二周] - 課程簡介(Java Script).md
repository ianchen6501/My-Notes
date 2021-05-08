# [第二周] - 課程簡介(Java Script)
### Java Script 的執行環境 (Runtime)
JS 需要有執行環境才能正確運作，目前來說主要有兩種就是
1. 瀏覽器 (google chrome / opera ...)
3. node.js
4. deno

執行環境可以當作一種編譯器，透過執行環境才可以正確的執行網頁程式。
接下來在不同執行環境中會有不同的 API 例如瀏覽器中會有 document.getElementById('idName') ，node.js 中有 fs ，然而在這兩個 runtime 當中可能彼此的 api 是不互通的(console 可以互通)。

### 網頁架構 - DOM (Document Object Model/物件文件模型)
- 在各家瀏覽器會有一個共同的網頁架構就是DOM。
- DOM是一個樹狀結構，其中會有不同的 nodes ，並有四種不同的 nodes ，分別是1. Doucument(就是這份 html 檔)、2. Elements (div、p等)、3.Text (就是被包裹起來的內容)、4. Attributes (屬性)

### console.log() 與 return 的差異
- console.log() 是輸出一個值
- return 是這個程式的回傳值

### 在瀏覽器執行 JavaScript
1. 用 terminal crate a new file called "index.html"
2. vim the file like
```
<script>
console.lg("helloworld")
</script>
```
3. open the file on browser
4. turn on the tool for users

###### tags: `week2`


