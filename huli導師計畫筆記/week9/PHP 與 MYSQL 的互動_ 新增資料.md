# PHP 與 MYSQL 的互動: 新增資料
### HULI 範例
```php
<?php
  require_once('conn.php');

  if (empty($_POST['username'])) {
    die('請輸入 username');
  }

  $username = $_POST['username'];
  $sql = sprintf(
    "insert into users(username) values('%s')",
    $username
  );
  $result = $conn->query($sql);
  if (!$result) {
    die($conn->error);
  }

  header("Location: index.php");
?>
```

### 示範流程
新增資料其實就是用 MYSQL 的 insert 指令
```php
<?php
require_once('conn.php');
//拿資料
$result = $conn->query("insert into users(username) values('apple')");
echo $result;
//檢查資料有無錯誤
if (!$result) {
  die($conn->error);
}
```
![](https://i.imgur.com/caLJt2F.png)
上面的結果會回傳 1 就是 true 的意思，表示資料新增成功
另外還有一個比較好的寫法是把插入的值獨立成一個變數，並用兩個""把斷句拆開
```php
<?php
require_once('conn.php');
//拿資料
$username = 'apple';
$sql = "insert into users(username) values('" . $username ."')"; //這邊注意分號的用法
echo $sql;
$result = $conn->query($sql);
print_r($result);

```
會發現已經可以成功傳入資料
![](https://i.imgur.com/yJWST6t.png)
另外也可以改成用 place hoder 的方式來做

```php
$sql = sprintf( //前面用 spintf() function
  "insert into users(username) values('%s')", $username //%s 是 place holder ，後面的變數會依序取代
);
```
當然我們也可以連同 id 一起新增
```php
$username = 'apple';
  $sql = sprintf( //前面用 spintf() function
    "insert into users(id, username) values(%d, '%s')",
    20, 
    $username //%s 是 place holder ，後面的變數會依序取代
  );
```
![](https://i.imgur.com/RRs0ReD.png)
現在我們可以實際做一次 insert 的動作,先寫一個 PHP insert 檔
```php=

<?php
require_once('conn.php');
//拿資料
if (empty($_POST['username'])) {
  die('請輸入 username');
}

$username = $_POST['username'];
  $sql = sprintf( //前面用 spintf() function
    "insert into users(username) values('%s')", 
    $username //%s 是 place holder ，後面的變數會依序取代
  );
echo 'SQL:' . $sql . '<br>';
$result = $conn->query($sql);
print_r($result);
//檢查資料有無錯誤，有錯就終止城市
if (!$result) {
  die($conn->error);
}
echo '新增成功'
?>
<!--新增一個回去的連結-->
<a href='data.php'>go back<a>
<!-- 在 header 增加一個回歸的 Location -->
header("Location: index.php");

```
然後另外用 form 來發出 request
```php=
<!--用 form 的方式新增資料-->
<?php
require_once('conn.php');
//拿資料
$result = $conn->query('SELECT * from users order by id DESC;'); 
//now() 也可用 * 取代，另外 order by id DESC (由大到小)、 ASC(由小到大)
//檢查資料有無錯誤
if (!$result) {
  die($conn->error);
}
//拿出已取得的資料，藉由 fetch_assoc() 取得相對應得資料
while($row = $result->fetch_assoc()) {
  echo 'id:' . $row['id'] . '<br>';
  echo 'username:' . $row['username'] . '<br>';
}
?>

<form method= 'POST', action='insert.php'>
  username: <input name='username'>
  <input type='submit' />
</form>
```
上面我們可以看到加入 header location 後，畫面會自動跳轉回 data.php，我們也可以透過 devtool 裡面看到同樣的狀況
![](https://i.imgur.com/vj97ttg.png)

###### tags: `week9`





