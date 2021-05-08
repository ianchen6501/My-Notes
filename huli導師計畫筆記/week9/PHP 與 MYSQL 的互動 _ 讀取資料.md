# PHP 與 MYSQL 的互動 : 讀取資料
### huli示範程式碼
```php
<?php
require_once('conn.php');

  $result = $conn->query("SELECT * FROM users");
  if (!$result) {
    die($conn->error);
  }

  while ($row = $result->fetch_assoc()) {
    echo "id:" . $row['id'] . '<br>';
    echo "username:" . $row['username'] . '<br>';
  }
?>
```

### query 資料方法
```php
<?php
require_once('conn.php');
//拿資料
$result = $conn->query('Select now() as n;'); //now() 也可用 * 取代
//檢查資料有無錯誤
if (!$result) {
  die($conn->error);
}
//拿出已取得的資料，藉由 fetch_assoc() 取得相對應得資料
$row = $result->fetch_assoc();
print_r($row);
echo '<br> now:' . $row['n'];



if(empty($_GET['name']) || empty($_GET['age'])) {
  echo '資料尚未填寫完成<br>';
  exit();
}
echo 'your name is :' . $_GET['name'] . '<br>';
echo 'your age is :' . $_GET['age'] . '<br>';
?>
```

### 實際範例
```php
<?php
require_once('conn.php');
//拿資料
$result = $conn->query('SELECT * from users;'); //now() 也可用 * 取代
//檢查資料有無錯誤
if (!$result) {
  die($conn->error);
}
//拿出已取得的資料，藉由 fetch_assoc() 取得相對應得資料，每一筆$row 可以取得一筆資料
$row = $result->fetch_assoc();
print_r($row);


if(empty($_GET['name']) || empty($_GET['age'])) {
  echo '資料尚未填寫完成<br>';
  exit();
}
echo 'your name is :' . $_GET['name'] . '<br>';
echo 'your age is :' . $_GET['age'] . '<br>';
?>
```
![](https://i.imgur.com/cODV5vx.png)
上面一筆一筆取的方式可以用 while 來取得每一筆資料
```php
<?php
require_once('conn.php');
//拿資料
$result = $conn->query('SELECT * from users;'); //now() 也可用 * 取代
//檢查資料有無錯誤
if (!$result) {
  die($conn->error);
}
//拿出已取得的資料，藉由 fetch_assoc() 取得相對應得資料
while($row = $result->fetch_assoc()) {
  print_r($row);
}
if(empty($_GET['name']) || empty($_GET['age'])) {
  echo '資料尚未填寫完成<br>';
  exit();
}
echo 'your name is :' . $_GET['name'] . '<br>';
echo 'your age is :' . $_GET['age'] . '<br>';
?>
```
```php
<?php
require_once('conn.php');
//拿資料
$result = $conn->query('SELECT * from users;'); //now() 也可用 * 取代
//檢查資料有無錯誤
if (!$result) {
  die($conn->error);
}
//拿出已取得的資料，藉由 fetch_assoc() 取得相對應得資料
while($row = $result->fetch_assoc()) {
  echo 'id:' . $row['id'] . '<br>';
  echo 'username:' . $row['username'] . '<br>';
}
if(empty($_GET['name']) || empty($_GET['age'])) {
  echo '資料尚未填寫完成<br>';
  exit();
}
echo 'your name is :' . $_GET['name'] . '<br>';
echo 'your age is :' . $_GET['age'] . '<br>';
?>
```
![](https://i.imgur.com/HaY0y1w.png)

###### tags: `week9`

