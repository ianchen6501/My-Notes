# CSS 基礎 - selector
### CSS - Cascading style sheets 階層式樣式表
---
- ### CSS selector
> selector {
    attributes : values
}
- ### style 的三種方式
1. 直接在段落標籤內加上 style

```htmlmixed=
<h1 style="background:red;"> 我是標題
</h1>
```
2. 在 header 加入 style 設定
```htmlmixed=
    <style>
      div{
      background:blue;
      }
    </style>
```
3. 另外開一個檔案 .css 並在 html 中引入
```htmlmixed=
    <link rel="stylesheet" href="./CSS_style.css">
```
```htmlmixed=
div{   <!-- .CSS-->
      background:blue;
      }
```
- ### CSS selector
1. universal selector : 全部都會被影響(不常用)
```htmlmixed=
*{
color:red;
}
```
2. 標籤 selector : 同樣的標籤都會被影響(不常用)
```htmlmixed=
div{
background:green;
}
```
3. id selector : 在標籤放入 id 並在 selector 搭配 #+id 名稱使用，單對單的使用(常用)
```htmlmixed=
<label id="name"> <!-- 設定 id ，記得加雙引號--> 
...
</label>
```
```htmlmixed=
#name {
    background:grey;
}
```
4. class selector : 用法很像 id selector，但為單對多的 selector，要搭配 .+classname 使用
```htmlmixed=
<label class1="name" class2="name"> <!-- 可以同時賦予多個 class 中間用 space 隔開 -->
...
</label>
```
```htmlmixed=
.classname1{
    backgorund:yellow;
}
.classname2{
    color:orange;
}
```
5. 同時符合 selector : 設定多個條件都符合才適用的 slelector 語法有兩種
```htmlmixed=
div.bg_yellow{ <!--同時符合 label = div & class = bg_yello-->
...
}
```
```htmlmixed=
.text_brown.bg_yellow{ <!--同時符合 class = text_brown & class = bg_yello，注意兩個都要搭配 . -->
...
}
```
6. 選到底下層的元素
```htmlmixed=
<div class="layer"> <!--多層 div 的狀況 -->
  hello
  <div>
    hello
    <div>
      hello
    </div>
  </div>
</div>
```
```htmlmixed=
.layer > div > div { <!-- 可以用 > 符號來選到"下一層"的內容 -->
      background: peru;
}
```
```htmlmixed=
.layer div{ <!-- 可以用 " " space 符號來選到裡面所有的內容 -->
      background: peru;
}
```
7. 選到旁邊的元素 
```htmlmixed=
<div>div1</div> <!-- div 跟 span 視作同一個 layer -->
<span>span1</span>
<span>span2</span>
```
```htmlembedded=
div + span { <!-- 用 + 可以選到 div 旁邊的 span1 -->
      background: peru;
}
```
```htmlembedded=
div ~ span { <!-- 用 + 可以選到 div 右邊的 span1 及 span2 -->
      background: peru;
}
```

- ### pseudo classes - hover
是一個假的 classes 可以做多種特效， hover 是較常用的用法，可以在滑鼠移上去的時候反白某種顏色或效果，另外可以在 devtool 裡面開啟 force element state 就可以強制開啟 hover 等效果
```htmlmixed=
div:hover { <!-- label 後面加 :hover -->
      background: peru;
}
```
- ### nth-child 選擇指定的部分
```htmlmixed=
<div>row1</div>
<div>row2</div>
<div>row3</div>
<div>row3</div>
<div>row5</div>
```
```htmlmixed=
.wrapper div:nth-child(2) { <!--選擇第 2 個元素-->
      background: peru;
}

.wrapper div:first-child { <!--選擇第 1 個元素-->
      background: peru;
}

.wrapper div:nth-child { <!--選擇最後個元素-->
      background: peru;
}

.wrapper div:nth-child(ever) { <!--選擇偶數個元素-->
      background: peru;
}

.wrapper div:nth-child(odd) { <!--選擇奇數個元素-->
      background: peru;
}
```
注意在 space 及 nth-child 同時存在時，系統其實是先看 nth-child 再判斷 space 後面的條件。
```htmlmixed=
      .wrapper div:nth-child(3) { <!-- 先看第 3 個是不是 div ，在看 space 後面的 div -->
            background: peru;
      }
```
()裡面也可以輸入運算式，如(3n)、(5n-1)等，系統會自動帶入0,1,2...並顯示符合的元素
- ### pseudo element 偽元素
利用 CSS pseudo element 的方式來添加內容，而且 psudo element 並不是 html 的元素。
```htmlmixed=
.at::before { <!-- 再 class:at 前面加上 "@" ，當然 before 可以改成 after -->
  content:"@"
}
```
也可以在目標的 label 裡面設定參數如 data-symbow ，之後可以在 content 利用 attr() 把參數給顯示出來
```htmlmixed=
<div>
  <span class="at" data-symbow="NTD">1000</span>
</div>

.at::after {
  content: attr(data-symbow)
}
```
- ### css selector 權重順序
1. 大原則
> id > class > 標籤(div、h、p)
> 越詳細越好
2. 計分制 : 實際上是比較各個順位的數量

| id | class / tseudo class | elements |
| -------- | -------- | -------- |
| 0     | 0    | 0     |

```htmlmixed=
#id1 #id2 { <!-- id:2 / class:0 / elements:0-->
...
}
```
```htmlmixed=
.class1 div { <!-- id:0 / class:1 / elements:1-->
...
}
```
```htmlmixed=
div.class1 > div.class2 { <!-- id:0 / class:2 / elements:2-->
...
}
```
3. inline style : 1,0,0,0
4. !important : 1,0,0,0,0

[強烈推薦收藏好物 – CSS Specificity (CSS 權重一覽)](https://muki.tw/tech/css-specificity-document/)
[你對 CSS 權重真的足夠了解嗎](https://juejin.im/post/5afa98bf51882542c832e5ec)

###### tags: `week6`