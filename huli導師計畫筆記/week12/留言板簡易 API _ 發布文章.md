# 留言板簡易 API : 發布文章
利用取得的 post 資料來執行 sql 指令，並回傳結果
```php
<?php
require_once('conn.php');
header('Content-Type: application/json; charset=utf-8');

//檢查有無提送資料
if (
  empty($_POST['content'])
) {
  $json = array (
    "ok" => false,
    "message" => "please input content"
  );
  $response = json_encode($json);
  echo $response;
  die();
}

$username = $_POST['username'];
$content = $_POST['content'];
$sql = "insert into comments(username, content) values(?, ?)";
$stmt = $conn->prepare($sql);
$stmt->bind_param('ss', $username, $content);
$result = $stmt->execute();
//檢查有無連線成功
if (!result) {
  $json = array(
    "ok" => false,
    "message" => $conn->error
  );
}

$response = json_encode($json);
echo $response;
die();
//回傳成功資訊
$json = array(
  "ok" => true,
  "message" => "success"
)
?>
```

###### tags: `week12`