# PHP 執行流程
![](https://i.imgur.com/rckYL0j.jpg)
動態網頁是利用 server 執行 php 檔案來達成，但不是每個 server 都有這樣子的功能，另外我們也可以透過在 html 裡面放入 PHP 程式碼，來達成某些動態更新功能
```htmlmixed=
<?php
echo "iamhuliyo"
?>
<h1>NOW: <?php echo date("y-m-d  h-i-s")?></h1>
```

###### tags: `week9`