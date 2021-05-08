# form 串接 API
> 可以透過直接在 html 利用 form 串接 API ，方法如下:
```htmlmixed=
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>form__api</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>

  </style>
</head>
<body>
  <form method="GET" action="http://google.com"> 
  <!--可以利用 GET / POST 等方法， action 加 api 位址-->
    <input name='username'>
    <input type="submit"/>
  </form>
  <script>
  </script>
</body>
</html>
```

###### tags: `week8`