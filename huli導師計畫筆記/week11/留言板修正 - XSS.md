# 留言板修正 - XSS
### 原因
透過在留言板留言輸入 js 語法，因為我們原本在寫時是把留言當作程式碼的一部分，因此可以透過輸入
``<script>alert("hacked")</script>``
``<script>alert(location.href="google.com")</script>``
``<script>alert(document.cookie)</script>``
等方式來取得資料或導到釣魚網站
### 解法
解決的方式是透過``htmlspecialchar(var, ENT_QUOTES)``這個函式來把輸出的內容轉譯為特殊符號別稱

###### tags: `week11`