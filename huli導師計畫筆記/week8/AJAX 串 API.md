# AJAX 串 API
### AJAX - Asynchronous JavaScript and XML
> （非同步的 JavaScript 與 XML 技術）的縮寫，簡單說就是網頁不用重新整理，就能即時地透過瀏覽器去跟伺服器溝通，撈出資料。

```htmlmixed=
  <script>
    //設變數以抓取資料
    const request = new XMLHttpRequest()
    //回傳資料後的 function
    request.onload = function() {
      if(request.status >= 200 && request.status < 400) {
        console.log(request.responseText) //成功回報
      } else {
        console.log('error')
      }
    }
    //回傳錯誤的 function
    request.onerror = function() {
      console.log('error')
    }

    request.open('GET', 'https://blog.techbridge.cc/2017/05/20/api-ajax-cors-and-jsonp/', true)
    request.send()
  </script>
```

```htmlmixed=
  <script>
    const request = new XMLHttpRequest()
    //可以改用 addeventlistener 的方式
    request.addEventListener('load', function() {
      if(request.status >= 200 && request.status < 400) {
        console.log(request.responseText)
      } else {
        console.log(request.status, request.responseText)
      }
    })

    request.onerror = function() {
      console.log('error')
    }

    request.open('GET', 'https://blog.techbridge.cc/2017/05/20/api-ajax-cors-and-jsonp/12345678', true)
    request.send()
  </script>
```

###### tags: `week8`

