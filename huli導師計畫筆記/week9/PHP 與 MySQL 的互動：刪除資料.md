# PHP 與 MySQL 的互動：刪除資料
### HULI 範例
```php=
<?php
  //連結 local host
  require_once('conn.php');
  //預防空白輸入
  if (empty($_GET['id'])) {
    die('請輸入 id');
  }
  //request method
  $id = $_GET['id'];
  $sql = sprintf(
    "delete from users where id = %d",
    $id
  );
  echo $sql . '<br>';
  $result = $conn->query($sql);
  if (!$result) {
    die($conn->error);
  }
  //回傳是否成功
  if ($conn->affected_rows >= 1) {
    echo '刪除成功';
  } else {
    echo '查無資料';
  }

  // header("Location: index.php");
?>
```

- 刪除做法與 insert 很像，主要變更部分是把 insert 改成 delete 語法，首先我們先把 data.php 新增一個刪除按鈕
```php
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
    echo 'id:' . $row['id'];
    echo "<a href='delete.php?id=" . $row['id'] ."'>刪除</a>" . '<br>';
    echo 'username:' . $row['username'] . '<br>';
  }
  ?>
  ```
- 接著把 Php request 部分改成 delete method
```php=
<?php
require_once('conn.php');
//拿資料
if (empty($_GET['id'])) {
  die('請輸入 id');
}

$id = $_GET['id'];
  $sql = sprintf( //前面用 spintf() function
    "DELETE FROM users WHERE id = %d", 
    $id //%d 是 place holder ，後面的變數會依序取代
  );
echo $sql;
$result = $conn->query($sql);
print_r($result);
//檢查資料有無錯誤，有錯就終止城市
if (!$result) {
  die($conn->error);
}

header("Location: data.php");
?>
<a href='data.php'>go back<a>
```
- 另外要注意的是假設我們 delete 一個不存在的 id ，還是會執行成功，對於資料庫來說刪除一個不存在的資料是合理的。
- 接著我們其實可以用判斷刪除之後影響幾列，來知道有沒有成功刪除存在的資料，用到的函數是 afffected_rows，會回傳影響幾列
```php=
echo $conn->affected_rows;
```
![](https://i.imgur.com/CCAPlVy.png)
- 所以我們可以透過判斷 affected_row 的數量來判斷是否有刪除成功
```php=
if ($conn->affected_rows >0) {
  echo '刪除成功';
} else {
  echo '刪除失敗';
}
```
![](https://i.imgur.com/HPcg1vw.png)

###### tags: `week9`

