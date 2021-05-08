# CSS 優化
### minify


### 前端優化
- 資源本身的大小
minify
gzip*
- 資源載入的方式
CSS sprites
Critical CSS
Cache*
- 資源執行的方式
選擇器
屬性渲染

### Critical CSS
- 把一個大的 CSS 載入(耗時)，拆成數個部分，先載入比較重要的部分，再載入比較不重要的部分。
![](https://i.imgur.com/0ziOfjK.png)
- 實際應用
1. 最簡單的方式是把原本在 style.css 裡面一開始使用者載入會看到畫面的 css 直接放在 html 檔裡面

### CSS Sprite
- 把數個小的 CSS 合併一併載入
![](https://i.imgur.com/AhWpn0P.png)
- 實際應用
1. svg reference
2. ㄧ般圖片檔 : 透過更改 ``background-position : x , y`` 來找到要匯入的圖片位置，其他的部分就 overflow 掉
![](https://i.imgur.com/40li250.png)

上述兩個要針對專案性質，視情況使用。

### 選擇器
- 避免過多的複雜選擇器(nth / sass 多重巢狀)

### 屬性渲染
- [render tree construction](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction)
- google core web vitals (LCP、FID、CLS)
- 注意網站在變化或做一些動畫時的渲染耗時表現，所以必須先深入了解那些屬性在動畫時會重繪及如何重繪(layout / composite layers)\

### cache
把已載入的東西暫存在 client 端。
![](https://i.imgur.com/JscKxk7.png)

###### tags: `week13` `CSS` `CSS sprite`