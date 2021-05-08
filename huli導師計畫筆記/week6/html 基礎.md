# html 基礎
- href / src / url
href 是指物件的路徑，src 是物件的來源，url 是連結的意思在 html 語法中不會用到

- 基礎元素
```htmlmixed=
<!DOCTYPE html>
<html lang = "en-US">
<head>
  <title></title>
  <meta charset="UTF-8">
  <meta name="description" content="description">
  <link>
  <script>
  <style> <!--注意 style 標籤要設置，不然 body 會沒有型式，不會顯示 --->
  <base>
</head>
<body>
<h1>小明的異想世界</h1>
<p> <p>    
</body>
</html>
```
- [loren ipsum](https://loremipsum.io) 用來產出無意義的文章，方便模擬文字區塊的內容

- 清單
```htmlmixed=
<ul> <!-- 無序清單-->
<li>hi</li>
<li>hi</li>
<li>hi</li>
</ul>
```
```htmlmixed=
<ol> <!-- 有序清單-->
<li>hi</li>
<li>hi</li>
<li>hi</li>
</ol>
```

- 保留完整格式(換行等)
```htmlmixed=
<bre> <!--預設的段落標籤不會顯示 space，要改用 bre 才能完整呈現。-->
  這是段落起點
     繼續縮排
</bre>
```
```htmlmixed=
<p>
我愛夏天<br> <!-- 在段落裡要換行要加上 br 標籤-->
我愛夏天<br>

</p>
```
- 表格 
<table><!--一個表格外面要用 table 標籤包起來-->
<tr> <!--每一 row (行) 要有一個 tr 標籤-->
<td>姓名</td><!--每一 row (行) 要有一個 tr 標籤-->
<td>蔬菜</td>
<td>水果</td>
</tr>
<tr> 
<td>小菜</td><!--每一個 row element 用 td 標籤-->
<td>高麗菜</td>
<td>橘子</td>
</tr>
<tr> 
<td>小田</td>
<td>花椰菜</td>
<td>蘋果</td>
</tr>
<tr> 
<td>小明</td>
<td>菠菜</td>
<td>火龍果</td>
</tr>
<tr> <!-- th 標籤會以粗體表示-->
<th>小送</th>
<th>A菜</th>
<th>腰果</th>
</tr>
</table>

- 錨點 anchor
第一種用法可以連到外部網站
```htmlmixed=
<a href="https://www.amazon.com" target='_self'>
<!-- target 預設為 _self ，意思是超連結會在本頁開啟-->
take me to amazone </a>

<a href="https://www.amazon.com" target='_blank'>

<!-- target 預設為 _blank ，會在新頁面開啟 -->
take me to amazone </a>
```
第二種用法是同一網頁的索引連結
```htmlmixed=
<a href="#p2">take me to p2</a>
<!-- href設定要去的錨點，記得要加 #-->
<p id="p1"> <!-- 在 p 標籤設定 id 可以當作去的港口鑰-->
... 一大串文字
</p>
<a href="p1">take me to p1</a>
<p id="p2">
... 一大串文字
</p>
```
- div
可以把各個部分包起來，被包起來的地方會變成獨立的部分，不在範圍內的內容會換行。
```htmlmixed=
<div>
<h1>
這是標題
</h1>
<p>
......
</p>
</div>
```
- sementic elements : 語意化標籤
功能大致與 div 相同，主要用意是為了讓閱讀的人或機器可以判讀段落的性質。
```htmlmixed=
<main> </main> <!-- 主要的部分 -->
<nav> </nav> <!-- 導覽列 -->
<footer> </footer> <!-- 底部的頁籤 -->
```
[更多的 sementic elements](https://www.w3schools.com/html/html5_semantic_elements.asp)
![](https://i.imgur.com/alQnPcu.png)

- iframe : 可以在頁面中嵌入別人的網頁，並直接使用其中的功能，大部分的知名網站都會擋，所以不常用
```htmlmixed=
<iframe src="https://loremipsum.io/generator/?n=5&t=p"
width="50" heigth="30"
</iframe>
```
- form 表單相關標籤
```htmlmixed=
<form>
  <div>
    編號:<input type="text"/> <!-- 單純的文字輸入框 -->
  </div>
  <div>
    密碼:<input type="password"/> <!-- 輸入內容會自動屏蔽 -->
  </div>
  <div>
    Email:<input type="email"/> <!--與 text 不同的地方在於，email送出會自動檢查是否符合 emial 格式-->
  </div>
  <div>
    <input type="date"/> <!-- 會有日期欄供選擇 -->
  </div>
  <div>
    生理性別: <input type="radio" name="gender" id="male"/><label for="male">男性</label> <!-- 單選框，要多重單選要把它用 name group 起來 -->
    <input type="radio" name="gender" id="female"/><label for="female">女性</label> <!-- 要讓文字也可以納入點選範圍，前後要用 label 包起來，並用 for 指向 id -->
    <input type="radio" name="gender" id="other"/><label for="other">其他</label> 
  </div>
  <div>
    興趣: <input type="checkbox" id="exercise"><label for="exercise">運動</label>
    <input type="checkbox" id="reading"><label for="reading">運動</label>
  </div>
  <div>
    <input type="submit" value="送出"/>
  </div>
```
[MDN input type](https://developer.mozilla.org/zh-TW/docs/Web/HTML/Element/input)

- **S**earch **E**ngine **O**ptimization 搜尋引擎最佳化
1. open graph protocol
> Open Graph Protocol 是 Facebook 在 2010 年提出，定義了的 HTML Meta Tag 中如何描述網頁的標題、縮圖、描述等資訊，不僅僅 Facebook 使用，現在越來越多的網站都支援 Open Graph Protocol。
常用的 Meta Tag
網頁標題：<meta property=”og:title” content=”網頁標題放這裡”/>
網頁描述：<meta property=”og:description” content=”網頁描述放這裡”/>
網頁類型：<meta property=”og:type” content=”網頁類型放這裡”/>
網頁縮圖：<meta property=”og:image” content=”網頁縮圖放這裡”/>
2. JSON LD - JSON for linking data 
> 也是一種基於 JSON 格式的 seo 描述文件。
```
{
  "@context": "https://json-ld.org/contexts/person.jsonld",
  "@id": "http://dbpedia.org/resource/John_Lennon",
  "name": "John Lennon",
  "born": "1940-10-09",
  "spouse": "http://dbpedia.org/resource/Cynthia_Lennon"
}
```
3. robots.txt : 給網頁爬蟲看的
通常位於根目錄，可以在網址後面加上"/robots.txt"查閱，主要內容會說明那些可以爬，那些不能爬，並有一些寫給 seo developer 的話。sitemap 是讓爬蟲了解，整個網站有哪些頁面需要爬。
```
User-Agent: *
Disallow: /m/
Disallow: /me/
Disallow: /@me$
Disallow: /@me/
Disallow: /*/edit$
Disallow: /*/*/edit$
Disallow: /media/
Disallow: /p/*/share
Disallow: /r/
Disallow: /t/
Disallow: /trending
Disallow: /search?q$
Disallow: /search?q=
Allow: /_/
Allow: /_/api/users/*/meta
Allow: /_/api/users/*/profile/stream
Allow: /_/api/posts/*/responses
Allow: /_/api/posts/*/responsesStream
Allow: /_/api/posts/*/related
Sitemap: https://medium.com/sitemap/sitemap.xml
```
- Escape : 跳脫，可以顯示標籤
"&"  --- &amp;
"<"  --- &lt;
">"  --- &gt;
```htmlmixed=
<div>
  &lt;div&gt;&lt;/div&gt;  &amp;
</div>
```
###### tags: `week6` 'html'