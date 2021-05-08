# 留言板簡易 API : 由 html 發出 request
[語法參考] (http://youmightnotneedjquery.com)
基本上重點在於，用 js/ajax 的方式去拿資料，不會用到 php 所以檔案附檔名可以改成 html 也沒差

```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>留言板</title>
  <link rel="stylesheet" href="style.css">
</head>

<body>
  <header class="warning">
    <strong>注意！本站為練習用網站，因教學用途刻意忽略資安的實作，註冊時請勿使用任何真實的帳號或密碼。</strong>
  </header>
  <main class="board">      
      <h1 class="board__title">comments</h1>
      <form class="board__new-comment-form">
        <textarea name="comments" rows="5"></textarea>
        <input type="hidden" name="id" value="<?php echo $row['id'] ?>" />
        <input class="board__submit-btn" type="submit" />
      </form>
      <section>

       </section>
  </main>
  <script>
    var request = new XMLHttpRequest();
    request.open('GET', 'api_comments.php', true);

    request.onload = function() {
      if (this.status >=200 && this.status <400) {
        var resp = this.response
        var json = JSON.parse(resp)
        var comments = json.comments
        for (let i = 0; i < comments.length; i++) {
          var comment = comments[i]
          var div = document.createElement('div')
          div.classList.add('card')
          div.innerHTML = `
            <div class='card__avatar'>
            </div>
            <div class='card__body'>
              <div class='card__info'>
                <span class='card__author'>
                  ${comment.username}
                </span> 
                <span class='card__time'>
                  ${comment.created_at}
                </span> 
                <p class='card__content'>
                  ${encodeHTML(comment.comments)}
                </p>   
              </div>
            </div>
          `
          document.querySelector('section').appendChild(div)
        }
      }
    }
    request.send();

    var form = document.querySelector('.board__new-comment-form')
    form.addEventListener('submit', function(e) { 
      e.preventDefault();
      var content = document.querySelector('textarea[name=comments]').value
      var request = new XMLHttpRequest();
      request.open('POST', 'api_add_comments.php', true)
      request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded; charset=UTF-8');
      request.send("username=ian&content=" + encodeURIComponent(content));
      request.onload = function() {
        var resp = this.response;
        var json = JSON.parse(resp);
        if (json.ok) {
          location.reload();
        } else {
          alert(json.message)
        }
      }
    })
    //xss escape function
    function encodeHTML(s) {
        return s.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/"/g, '&quot;');
    }


  </script>
  
</body>
</html> 
```

###### tags: `week12`