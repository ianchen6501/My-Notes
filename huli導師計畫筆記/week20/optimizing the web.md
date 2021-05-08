### optimizing the dom
- minify
- compress the file 
- cashe by the browser

### blocking CSS
因為 render 是產生 DOM -> CSSOM 才 render ，所以所有下載 CSS 的階段都會影響後面的 render 這就是 blockg render，但針對 @media 的部分，我們可以試著把不同 media 的檔案拆分開來，這樣雖然這些檔案會被 browser 下載，但卻不會進行 render

### JavaScript engine
觀察下面的 code 當 html DOM render 到 script 的時候會等 JS 載入檔案並解析完才會繼續跑，所以要避免這種行為。
```html
<p>
Awesome page
<script> with JavaScirpt </script>
is awesome
</p>
```
那假若在 DOM / CSS 載入時遇到 script ， browser 會先等 DOM tree / CSSOM 執行完在進行 JS 指令。注意這邊如果是非同步指令，browser 可以同步進行 parse 跟 JS。
- blocking
- inline
- async

### 小結
#### minify, Compress, cache
- HTML、CSS、Javascript
#### minimize use of render blocking resorurces (CSS)
- use mediaqueries on <link> to unblock rendering
- inline CSS (行內樣式，直接在 html 裡面執行)
#### minimize use of parsor blocking resources
- defer JavaScript exeption
- use async attribution on script
#### 3 buckets
1. minize bytes
2. reduce the number of critical resources 
3. shorten CRP length

#### which optimization strategies should be consider?
 - inline CSS / inline JS 但要考慮不同分頁適用性
 - media query for CSS
 - async JS 這邊連同 CSS要考慮 lazy load 會不會影響 DOM / CSSOM 的 render 結果

#### preloader