# flex
- flex 是 display 的一種屬性，可以分成 外容器(container)及內元件(items)
- container 的屬性
> display
flex-flow : flex direction 和 flex wrap 的縮寫
flex-direction : 用來改變軸線方向
( row | row-reverse | column | column-reverse )
flex-wrap : 用來決定超出範圍時，是否換行
( nowrap | wrap | wrap-reverse )
justify-content : 主軸的對齊設定
( flex-start | flex-end | center | space-between | space-around )
align-items : 交錯軸的對齊設定
( flex-start | flex-end | center | baseline | stretch )

- items 的屬性
> flex
flex-grow : 元件的伸展性，透過改變數值大小來改變不同元素伸縮的比重
flex-shrink : 同上，不過是改變伸縮性
flex-basis
order : 可以重新定義元件的排列順序
align-self : 調整內元件交錯軸的對齊設定(主軸線則不能另外做設定)，且可以個別設定單一元件的值。

- flex 宣告，一開始要宣告 flex 才可以作用(或宣告 inline-flex)
```css
.flex-container {
  display: flex | inline-flex;
}
```






[圖解：CSS Flex 屬性一點也不難](https://wcc723.github.io/css/2017/07/21/css-flex/)



###### tags: `week6` `flex`