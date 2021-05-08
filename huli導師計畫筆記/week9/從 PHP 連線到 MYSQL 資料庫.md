# 從 PHP 連線到 MYSQL 資料庫
透過 MYSQL admin 建立一個新的使用者及資料庫，並從 PHP 連線到 MYSQL 
```php
<?php
$server_name = 'localhost';
$username = 'ian';
$password = 'ian';
$dbname = 'ianoo';
//用mysqli 跟 database 建立連線，建立連線後的資料會回傳給$conn
$conn = new mysqli($server_name, $username, $password, $dbname);
//變數要存取屬性時用 -> 符號
if (!empty($conn->connect_error)) {
  echo '資料庫連線錯誤 ' . $conn->connect_error . '<br>';
}
?>
```
這邊錯誤的回傳指令也可以改用 die ，die 會 print 出錯誤訊息，並停止之後的指令
```php
<?php
$server_name = 'localhost';
$username = 'ian';
$password = 'ian';
$dbname = 'ianoo';
//用mysqli 跟 database 建立連線，建立連線後的資料會回傳給$conn
$conn = new mysqli($server_name, $username, $password, $dbname);
//變數要存取屬性時用 -> 符號
if (($conn->connect_error)) {
  die('資料庫連線錯誤 ' . $conn->connect_error . '<br>');
}
?>
```
ㄧ般來說，會建立一個 conn.php 的檔案來建立與資料庫的連線，然後另外用 require_once 來引入該檔案進行連線
```php
<!--連線檔案-->
<?php
$server_name = 'localhost';
$username = 'ian';
$password = 'ian';
$dbname = 'ian';
//用mysqli 跟 database 建立連線，建立連線後的資料會回傳給$conn
$conn = new mysqli($server_name, $username, $password, $dbname);
//變數要存取屬性時用 -> 符號
if (!empty($conn->connect_error)) {
  die('資料庫連線錯誤 ' . $conn->connect_error . '<br>');
}
?>
```
```php
<!--實際 request 的內容-->
<?php
require_once('conn.php');
if(empty($_GET['name']) || empty($_GET['age'])) {
  echo '資料尚未填寫完成<br>';
  exit();
}
echo 'your name is :' . $_GET['name'] . '<br>';
echo 'your age is :' . $_GET['age'] . '<br>';
?>

```

huli 示範檔案
```php=
<?php
  $server_name = 'localhost';
  $username = 'huli';
  $password = 'huli';
  $db_name = 'huli';

  $conn = new mysqli($server_name, $username, $password, $db_name);

  if ($conn->connect_error) {
    die('資料庫連線錯誤:' . $conn->connect_error);
  }
//設定正確的編碼與時區，避免中文亂碼
  $conn->query('SET NAMES UTF8');
  $conn->query('SET time_zone = "+8:00"');
?>

```

###### tags: `week9`