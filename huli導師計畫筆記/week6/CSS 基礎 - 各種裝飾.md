# CSS 基礎 - 各種裝飾
- background : 設定背景顏色
```css
#box1 {
  background: red;
}

#box2 {
  background: #8a5a5a;
}

#box3 {
  background: rgb(244, 40, 100);
}

#box4 {
      background: rgb(244, 40, 100, 0.5);
    }
    
#box5 { <!-- 以背景當作圖片 -->
  background: url(./test.jpg) no-repeat center bottom;
  height: 300px;
  background-size: contain / cover / 50% / 100px;
}
```
- border : 設定邊框，根據邊框的寬度會改變整體大小及內容位置，可以設定邊框樣式、顏色等
```css
#box1 {
  background: red;
  border: 30px solid green;
  height: 50px ;
}
```
- outline : 也是設定邊框，但是從內容物的外面開始長，所以不會改變整體大小及內容位置
```css
#box1 {
  background: red;
  outline: 20px green;
  width :50px;
  height: 50px;
}
```
- padding : 也是設定邊框，但無法改變顏色、樣式，顏色會比照 background 的顏色
```css
#box1 {
  background:orange;
  width: 100px;
  height: 100px;
  padding: 20px 10px; <!-- 可以改用 padding-left 等設定單邊-->
}
```
- margin : 設定與旁邊的距離，類似透明邊框的效果
```css=
#box2 {
  background:orange;
  width: 100px;
  height: 100px;
  margin: 20px;
}
```

- 文字相關設定 : 
```css=
#box1 {
  background:orange;
  border: 100px solid gray; /*垂直置中要靠 border / padding / line-height 來調整 */
  width: 500px;
  color: white; /*也可以採用 rgba 法*/
  word-break: break-all; /*文字是否斷行方法*/
  word-wrap: normal; /*文字斷行方法*/
  font-size: 30px;
  font-weight: bold; /*也可以輸入 100 - 900*/
  font-family: Arial, Helvetica, sans-serif;
  letter-spacing: 5px; /*字距*/
  line-height: 1.5em; /*行高*/
  text-align: center; /*水平置中*/
}
```
- overflow / text-overflow : 調整內容及文字內容超出的顯示方式
```css
  overflow: hidden; /*內容超出範圍的處理方式*/
  text-overflow: ellipsis; /*文字超出範圍的處理方式，要搭配 white-space: nowwrap; overflow: hidden; 一起使用*/
```
- box-shadow : 陰影設定
```css
/* offset-x | offset-y | blur-radius | spread-radius | color */
box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);
```
- transition : 設定物件狀態改變的秒數、變化方式等，如滑鼠移上去時
```css
#box1 {
  background-color: white;
  color: black;
  height: 100px;
  width: 200px;
  border: 5px solid gray;
  border-radius: 30px;
  font-family: monospace;
  font-weight: 800;
  text-align: center;
  line-height: 200px;
  transition: all 0.1s ease-in;
}

#box1:hover {
  background-color: white;
  color: black;
  height: 100px;
  width: 200px;
  border: 5px solid gray;
  border-radius: 30px;
  font-family: monospace;
  font-weight: 800;
  text-align: center;
  line-height: 200px;
  transition: all 0.1s ease-in;
}

```

- transform : 設定各種前後狀態改變效果，如放大、位移等
```css
#box1 {
  background-color: white;
  color: black;
  height: 100px;
  width: 200px;
  border: 5px solid gray;
  border-radius: 30px;
  font-family: monospace;
  font-weight: 800;
  text-align: center;
  line-height: 100px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-100px , -50px); /* transform 拿來當置中工具 */
}
#box1:hover {
  background-color: white;
  color: black;
  height: 100px;
  width: 200px;
  border: 5px solid gray;
  border-radius: 30px;
  font-family: monospace;
  font-weight: 800;
  text-align: center;
  line-height: 100px;
}
```
- box model : content / padding / border / margin area
一般預設的 box-sizing 是 content-box 但通常實際比較常用的是 border-box 才好來控制整體呈現的寬高(不會隨著加了 padding / border 而改變)。
```css
#box1 {
  font-size: 50px;
  box-sizing: border-box;
  background-color: blue;
  width: 150px;
  height: 150px;
  border: 5px solid brown;
  padding: 10px;                                         
  }
```

- Dispaly : 三種不同的畫面呈現方式，在處理的是 a.元素與相鄰元素的關係 b.元素內部的排列方式
> aaaa 水平排列

> a
> a
> a
> a 垂直排列

1. block: 一次會占掉一個橫幅的區塊，包含 div / h1 / p，可以設定元素的長寬高
2. inline: 會在同一個橫幅水平排列出現，包含 span / a，不可以設定寬高，或說設定了只會影響 border 的範圍
3. inline-block: 同時具備 inline 和 block 的特性，可以同幅並列並設定高度，如 input
4. none: 不顯示


```css
.box {
  background:orange;
  width: 100px;
  height: 100px;
  padding: 10px;
  display: inline-block;
}
```

- position : 
先搞懂定位點，排版的定位點大致可分為 依照 a.排版流依序排列(static) / b.對自身定位(relative) / c.對viewport定位(fixed) / d.對上一個非 static 的元素定位(absolute)，然後這些定位就可以分為 相對定位(a.b) 及 絕對定位(c.d)
1. static : 預設，就是按照物件的性質(block / inline / inline-block)來排列
2. relative : 以自身的原始位置為原點來移動
3. fixed : 固定在畫面的特定位置(相對於 viewport 做定位)，就算畫面上下滑動也不會改變位置。
4. absolute : 以"某個參考點"為定位來移動，某個參考點是以該元素以上找第一個設定不是 stastic 的元素。值得注意的是，當元素設定為 absolute 的時候會跳脫原始多行文字的排序，後面的文字會遞補上來(relative 不會)

- Z-index : 調整元素的顯示前後順序，
> z-index: 10; 數字用來表示排序

- sticky : 讓元素碰到邊界時會隨著滑動移動，可以設定邊距(top / bottom ....) ，注意要設計邊距才會有作用。

###### tags: `week6`