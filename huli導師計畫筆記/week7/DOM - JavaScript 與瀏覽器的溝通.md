# DOM - JavaScript 與瀏覽器的溝通

### DOM = Document Object Model
### DOM 是 html 和 javascript 之間的橋梁，透過把 html 裡面的 element 轉換成物件的形式，最後就會形成一個樹狀結構
### DOM的節點:
1. Document
2. Element
3. Text
4. Attribute
### DOM API
document.getElementById('idName')
找尋 DOM 中符合此 id 名稱的元素，並回傳相對應的 element 。

document.getElementsBytagName('tag')
找尋 DOM 中符合此 tag 名稱的所有元素，並回傳相對應的 element 集合，集合為 HTMLCollection 。

document.getElementsByClassName('className')
找尋 DOM 中符合此 class 名稱的所有元素，並回傳相對應的 element 集合，集合為 HTMLCollection 。

document.querySelector('selector')
利用 selector 來找尋 DOM 中的元素，並回傳相對應的第一個 element 。

document.querySelectorAll('selector')
利用 selector 來找尋 DOM 中的所有元素，並回傳相對應的第一個 element ，集合為 NodeList 。
### 改變元素的 CSS
先利用 DOM API 來呼叫元素後，就可以透過來更動 CSS 的設定
```javascript=
const elements = document.querySelector('div')
elements.style.background='green';
elements.style.paddingButtom='10px';
//注意有些 CSS attribute 命名中如果有 '-' 符號要改成駝峰命名或以['']來取代
```

### 改變元素的 Class
```htmlmixed=
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>The HTML5 Herald</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src='./1.js'></script>
  <style> /*設定一個新的 CSS style*/
    .active { 
      background: red;
    }
  </style>
</head>
<body>
  <div class='block'>
    hihihi
  </div>
  <script>
    const elements=document.querySelector('.block')
    elements.classList.add('active') /*新增 Class */
    elements.classList.remove('block') /*刪除 Class */
    elements.classList.toggle('active') /*class 開關 */
  </script>
</body>
</html>
```

### 改變內容 : innerText、innerHTML、outerText、outerHTML
```htmlmixed=
<body>
  <div class='block'>
    hihihi
    <a>hello~</a>
  </div>
  <script>
    const elements=document.querySelector('.block > a');
    console.log(elements.innerText); /*印出內部不含本體的內容*/
    elements.innerText='你好嗎?'; /*改變內容*/
    
    console.log(elements.innerHTML); /*印出 html 內容*/
    elements.innerHTML='<h1>愛妳喔</h1>'; /*改變內容*/
  </script>
</body>
```
```htmlmixed=
<body>
  <div class='block'>
    hihihi
    <a>hello~</a>
  </div>
  <script>
    const elements=document.querySelector('.block > a');
    console.log(elements.outerText); /*印出含本體的內容*/
    elements.outerHTML='<h1>i am a pig!</h1>' /*改變內容*/
  </script>
</body>
```
### 刪除元素及插入元素
```javascript=
  <script>
    const element=document.querySelector('#block');
    element.removeChild(document.querySelector('a'))
  </script>
```
```htmlmixed=
  <script>
    const element=document.querySelector('#block');
    const item = document.createElement('div')
    item.innerText='123'
    element.appendChild(item)
  </script>
```

[HTML DOM 查詢](https://www.w3schools.com/jsref/dom_obj_attributes.asp)

###### tags: `week7` `DOM`