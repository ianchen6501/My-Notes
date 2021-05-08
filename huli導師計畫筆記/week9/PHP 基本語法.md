# PHP 基本語法
```php=
<?php //要用這個標籤包起來，可省略php但部分瀏覽器不支援，所以不建議
    $A=1; //宣告變數，所有程式碼後面要用 ; 結尾
    echo $A . '<br>'; //印出變數
    $B='這是字串';//亦可宣告字串
    echo $B . '<br>';

    $C='字串';
    $D='拼接';
    echo $C . $D . '<br>'; //字串拼接用 .

    //基本if語法
    $score = 60;
    if ($score >= 60) { //基本上可以把 $score 看做一個變數
      echo 'pass<br>';
    } else {echo 'fail . <br>';}

    //基本迴圈語法
    for ($i=0; $i<10; $i++) {
      echo $i . "\n"; //查看程式碼的確有換行，但沒換行原因如下
    }
    for ($i=0; $i<10; $i++) {
    echo $i . '<br>'; //因為目前解析環境是瀏覽器所以換行必須要用 <br>
    }

    //array
    $array = [1, 2, 3, 4, 'hihi'];
    echo 'length:' . sizeof($array) . '<br>'; //用 sizeof 可以取得 array length
    echo $array[sizeof($array) - 1] . '<br>'; //拿到第五個 element
    echo var_dump($array) . '<br>'; //array 無法直接被印出，要用 var_dump 函數來印出，會同時印出 type / value 
    echo print_r($array) . '<br>'; //僅會印出值

    //function
    function add ($a, $b) {
      return $a + $b;
    }
    echo add(2, 5);
?>
```

###### tags: `week9`