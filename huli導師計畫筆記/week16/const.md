# const
### constant
等於賦予一個不可改變的值，所以這邊也會有兩個不同情形。
1. primitive type 如果今天是改變值的話，會出現 error
```javascript=
const a = 10
a = 20 //error
```
2. object 如果有變更到記憶體位置，也會出現 error
```javascript=
const a = {
  number : 10
}
a.number = 20
a = {
  number : 20
}
```
如果只有變更該記憶體位置內的值的話，則不會 error
```javascript=
const a = [1, 2, 3]
a[0] = 4 //ok
```

###### tags: `week16` `const`