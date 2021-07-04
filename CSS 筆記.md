### display
- inline-block 如果彼此之間有 tab 或換行預設會有間隙，解法可以用 ``float: left``或刪除 span tag 中的空格	

### Typical Device Breakpoints
/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {...}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {...}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {...}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {...}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {...}

- min-width

--- 
## CSS
### 瀏覽器字首
-webkit- WebKit系瀏覽器(Chrome、Safari私有屬性)
-moz- Gecko系瀏覽器(Mozilla、Firefox私有屬性)
-o- Opera瀏覽器
-ms- IE瀏覽器私有屬性

### font-family
- 分為指定字體及泛用字體
- 指定字體放前面，泛用字體放最後一個
- 指定字體越前面，優先級越高
microsoft: 
``ont-family: "微軟正黑體", "Microsoft JhengHei", "Segoe UI Semibold", "Segoe UI", "Lucida Grande",``


### 元件狀態
:active 滑鼠按下的樣式
:focus 鍵盤聚焦的樣式
:hover 滑鼠滑過的樣式
:link 還沒被訪問的樣式
:visited 被訪問過的樣式

### chebox status
``checked = {true / false}`` checked 屬性可以用來判斷勾選與否

### 文字相關
- word-break
超出文本內容時是否換行
normal / break-all / keep-all
- word-wrap
單字過長換行的設定，也可以加上 ``&shy;`` 來讓文字換行並加上 - 符號
normal / break-word / initial / inherit

- text-overflow
clip / ellipsis / "-" / ""
會讓過長的文字顯示 `...`，要搭配 `overflow: hidden;` 使用，如果要一行直接斷行，要另外使用 `white-space`

- white-space
控制整段文字的換行
/* Keyword values */
white-space: normal;
white-space: nowrap;
white-space: pre;
white-space: pre-wrap;
white-space: pre-line;

/* Global values */
white-space: inherit;
white-space: initial;
white-space: unset;

### initial / inherit / unset
-   initial  
    將此屬性值恢復為瀏覽器預設值．  
    備註：所有 browser 都有自己的一套預設樣式，就像 input 在[各 browser 都長不一樣](https://css-tricks.com/numeric-inputs-a-comparison-of-browser-defaults/)是相同的道理
-   inherit  
    繼承 parent 的設定值
-   unset  
    如果 parent 有設定此屬性值則 `inherit` ，反之則 `initial`
	
### img
#### div_background-image
- background-image: url('img_girl.jpg');
- background-repeat: no-repeat;
- background-attachment: 
設定圖片的定位方式，預設為 `scroll`
scroll: 圖片會隨著外層 scroll 移動，意思當你外面 scroll 的時候圖片會看到同一個部分，內層 scroll 時不會跟著移動
fixed: 圖片不會隨著外層 scroll 移動，但內層 scroll 時不會跟著移動
local: 圖片會隨著內、外層 scroll 移動
- background-size: cover;
- background-position: 
設定圖片的定位位置

img 下面會有縫隙因為 inline 或 inline-block 預設會跟 parent vertical-align:basement 對齊，所以必須把 img 改 block 或調整 vertical-align:top | bottom | middle 
