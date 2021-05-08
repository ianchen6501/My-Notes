# DOM - JavaScript 網頁事件處理

### EventListener / Callback function
EventListener 可以用來偵測各種不同行為，包含
> click: 滑鼠點擊
> scroll: 滑鼠埢軸
> keydown: 鍵盤
> submit: 送出
```htmlmixed=
  <script>
    const element=document.querySelector('#block');
    element.addEventListener('click', onClick)
    function onClick() { /*callback function*/
      alert('click')
    }
  </script>
```
or
```htmlmixed=
  <script>
    const element=document.querySelector('#block');
    element.addEventListener('click', function() {
          alert('click')
    })
  </script>
```
### 我們也可以透過監聽來獲得各種使用者行為資訊
```htmlmixed=
  <script>
    const element=document.querySelector('#block');
    element.addEventListener('click', function(e) { /*e = event*/
      console.log(e.target) /*回傳就是事件的目標*/
    })
  </script>
```
```htmlmixed=
  <script>
    const element=document.querySelector('#block');
    window.addEventListener('keydown',function(e){
      console.log(e.key)
    })
  </script>
```
這邊有一個把背景變成紅色的小範例，流程是監聽 click 然後選到 body 改變 body 的 css style 
```htmlmixed=
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>The HTML5 Herald</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    .active {
      background: red;
    }
  </style>
</head>
<body>
  <div id='block'>
    yo
    <a>hello~</a>
  </div>
  <input/>
  <button class='change-btn'>
    red
  </button>
  <script>
    const element = document.querySelector('.change-btn')
    element.addEventListener('click',function(){
      document.querySelector('body').classList.toggle('active')
    })
  </script>
</body>
</html>
```
### 表單事件處理
```htmlmixed=
<body>
  <form class='form-login'>
    <div>
      username: <input name='username'/>
    </div>
    <div>
      password: <input name='password' type="password"/>
    </div>
    <div>
      password again: <input name='password2' type="password"/>
    </div>
    <input type="submit"/>
  </form>
  <script>
    const element = document.querySelector('.form-login')
    element.addEventListener('submit', function(e){
      alert('submit!') /*submit 後就會跳出 submit! 訊息*/
    })
  </script>
</body>
```
### preventDefault
如果不想提交，可以利用 preventDefault()來阻止預設的行為
```htmlmixed=
  <script>
    const element = document.querySelector('.form-login')
    element.addEventListener('submit', function(e){
      e.preventDefault()
    })
  </script>
```
用 if 來驗證前後密碼是否一致
```htmlmixed=
  <script>
    const element = document.querySelector('.form-login')
    element.addEventListener('submit', function(e){
      const input1 = document.querySelector('input[name=password]')
      const input2 = document.querySelector('input[name=password2]')
      if (input1.value !== input2.value) {
        alert('前後密碼不一致')
      }
    })
  </script>
```
防止 input 輸入某些字元
```htmlmixed=
  <script>
    const element = document.querySelector('input')
    element.addEventListener('keypress', function(e){
        if (e.key ==='e') {
          e.preventDefault()
      }
    })
  </script>
```

###### tags: `week7`