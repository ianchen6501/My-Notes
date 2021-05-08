# 留言板簡易API : 列出文章
```php
<?php
require_once('conn.php');

//設定留言分頁及每頁筆數
$page = 1;
if (!empty($_GET['page'])) {
  $page = intval($_GET['page']);
}
$items_per_page = 5;
$offset = ($page - 1) * $items_per_page;

//拿到所有 comments 資料
$stmt = $conn->prepare(
  'select '.
  'C.id as id, C.comments as comments, '.
  'C.created_at as created_at, U.nickname as nickname, U.username as username, U.authority as authority '.
  'from Ian_comments as C ' .
  'left join Ian_users as U on C.username = U.username '.
  'where C.is_deleted IS NULL '.
  'order by C.id desc ' .
  'limit ? offset ? '
);
$stmt->bind_param('ii', $items_per_page, $offset);
$result = $stmt->execute();
if (!$result) {
  die($conn->error);
}
$result = $stmt->get_result();

$comments = array();
//取得回傳資料
while ($row = $result->fetch_assoc()) {
  array_push($comments, array(
  "id" => $row['id'],
  "username" => $row['username'],
  "nickname" => $row['nickname'],
  "comments" => $row['comments'],
  "created_at" => $row['created_at']
  ));
}

$json = array(
  "comments" => $comments
);

//回傳 json 的 header 用來告訴瀏覽器回傳的格式

$response = json_encode($json);
header('Content-Type: application/json; charset=utf-8'); 
echo $response;

?>

```
![](https://i.imgur.com/fMFXx9K.png)
其中 nickname 的編碼之後 json 會自動轉譯


###### tags: `week12`