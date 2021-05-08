	### Cause
在 1 to many 的資料庫結構中，如果我們要選中各個物件中的子物件，會出現一筆一筆搜尋的狀況。在 mysql 的資料檢索作業中，一筆指令搜尋多個物件會來的比多筆搜尋一個物件的狀況來的有效率，所以我們必須盡可能避免 N + 1 query 的狀況。

### Example
```js
$cats = load_cats();
foreach ($cats as $cat) {
  $cats_hats = load_hats_for_cat($cat);
  // ...
}
```

```js
SELECT * FROM cat WHERE ...
```

```js
SELECT * FROM hat WHERE catID = ...
```

```js
SELECT * FROM cat WHERE ...
SELECT * FROM hat WHERE catID = 1
SELECT * FROM hat WHERE catID = 2
SELECT * FROM hat WHERE catID = 3
SELECT * FROM hat WHERE catID = 4
SELECT * FROM hat WHERE catID = 5
...
```

### eager loading
要解決 N + 1 probloem 可以利用 eager loading 預先加載的方式

```js
$cats = load_cats();
$hats = load_all_hats_for_these_cats($cats); //eager loading
foreach ($cats as $cat) {
  $cats_hats = $hats[$cat->getID()];
}
```

```js
SELECT * FROM cat WHERE ...
SELECT * FROM hat WHERE catID IN (1, 2, 3, 4, 5, ...)
```