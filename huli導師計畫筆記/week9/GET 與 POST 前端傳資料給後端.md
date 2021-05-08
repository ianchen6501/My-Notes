# GET 與 POST 前端傳資料給後端
### GET
```php
<?php
echo 'Hello I am ian. <br>';
//可以用 $_GET 方法來取得傳入前端傳入的資料
echo 'a:' . $_GET['a'] . '<br>';
echo 'b:' . $_GET['b'] . '<br>';
print_r($_GET);
?>
```
![](https://i.imgur.com/l6pKW3Z.png)

上述如果 a.b 沒有傳進來會出現提示訊息，所以可以透過 isset 來避免這樣的狀況
```php
<?php
echo 'Hello I am ian. <br>';
if (isset($_GET['a'])) {
  echo 'a:' . $_GET['a'] . '<br>';
}
if (isset($_GET['b'])) {
  echo 'b:' . $_GET['b'] . '<br>';
}
print_r($_GET);
?>
```
![](https://i.imgur.com/fHxBCrj.png)

但 isset 主要是來判斷是否有變數卻無法判斷空字串的情形，所以應該另外用 empty 函數來判斷空字串。
```php
<?php
echo 'Hello I am ian. <br>';
if (empty($_GET['a'])) {
  echo 'a: empty<br>';
} else {
  echo 'a:' . $_GET['a'] . '<br>';
}
if (isset($_GET['b'])) {
  echo 'b: empty<br>';
} else {
  echo 'b:' . $_GET['b'] . '<br>';
}
print_r($_GET);
?>
```
![](https://i.imgur.com/r94tnhN.png)
所以我們其實可以另建一個新檔建立一個傳送 GET 的表單，在由原本的 PHP 檔接收後並回傳
```htmlmixed=
<!-- GET 表單 -->
<form method='GET' action='GetPost.php'>
name: <input name='name'/>
age: <input name='age'/>
<input type='submit'/>
</form>
```
![](https://i.imgur.com/hoH0kHk.png)
```php
<!-- php 回傳 -->
![](https://i.imgur.com/YR6bUBb.png)
```

### POST
POST 會打包資料傳送過去，以上面的例子為例，如果我們把 GET 方法改為 POST
並發送，會得到下面情形，php 沒辦法正確處理資料
```htmlmixed=
<form method='POST' action='GetPost.php'>
name: <input name='name'/>
age: <input name='age'/>
<input type='submit'/>
</form>
```
![](https://i.imgur.com/GBHjftm.png)
這時如果我們打開 devtool 來看，會發現其實 method 改成 POST ，並傳送了資料
![](https://i.imgur.com/eihXgPx.png)
![](https://i.imgur.com/4R5NUHK.png)
所以我們必須改成 $_POST 的方法來取得資料，就成功了
```php
<?php
if (empty($_POST['name']) || empty($_POST['age'])) {
  echo '資料尚未填寫完成<br>';
  exit();
}
echo 'your name is :' . $_POST['name'] . '<br>';
echo 'your age is :' . $_POST['age'] . '<br>';
?>
```
![](https://i.imgur.com/q1Y5Jwl.png)

另外其實 GET 跟 POST 方法可以混用，但不建議
```htmlmixed=
<form method='POST' action='GetPost.php?school=ncku'>
<!--網址要補上 ?school=ncku -->
name: <input name='name'/>
age: <input name='age'/>
<input type='submit'/>
</form>
```
```php
<?php
if (empty($_POST['name']) || empty($_POST['age'])) {
  echo '資料尚未填寫完成<br>';
  exit();
}
echo 'your name is :' . $_POST['name'] . '<br>';
echo 'your age is :' . $_POST['age'] . '<br>';
echo 'your school is ' . $_GET['school'] . '<br>';
?>
```
![](https://i.imgur.com/HRhwsnb.png)

###### tags: `week9`


