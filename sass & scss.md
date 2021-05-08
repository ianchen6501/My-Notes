## scss
### variable
variable 用 $ 來命名，型態可以是 string / null / boolean 趁至 lists 或 Maps //這邊不是很懂
```js
$variable : ...,
```

### nesting
降低 parent 的重複性
```js
.parent {
  color: blue;
  .child {
    font-size: 12px;
  }
}
```
也可以用在相同 property 上面
```js
.parent {
  font: {
    size: 12px,
	color: green,
    family: sens-sarif,
  }
}
```

### mixings
降低 pseudo element 的重複性，在 scss 裡面 & 代表 parent
