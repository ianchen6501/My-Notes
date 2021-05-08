# [第二周] - JavaScript 判斷式
### 註解
```javascript=
//這是單行註解
/*這是多行註解 
 */
```


### 判斷式的基本簡介
- 判斷式的語法
```javascript=
if (判斷句)
    {執行的項目  
    }
else
    {執行的項目  
    }
```
```javascript=
if (判斷句)
    {執行的項目  
    }
else {if(){
    }
    }
```
```javascript=
if (判斷句)
    {執行的項目  
    }
else if(判斷句)
    {執行的項目  
    }
else
    {執行的項目  
    }
```
![](https://i.imgur.com/2FnB2Jr.jpg)
- 判斷的條件如果有兩個以上，要用 && 或 || 等連接
```javascript=
var a = 60
if (a>=20 && a<=40){
    console.log(appropriate)
}
else {
    console.log(imappropriate)
}

```
- Switch case
如果同時有多個判斷條件也可以用 swich case ，語法如下:
```javascript=
var ChineseZodiac = 1
switch(ChineseZodiac){
    case 1:
    console.log(鼠)
    break //注意要加 break 才會在該行停止不然會一直跑下去
    case 2:
    console.log(牛)
    break
    ...
    default: 
    console.log(no match)
}
```
- switch case vs array
```javascript=
var month = 5
switch (month){
    case 1:
    console.log(一月)
    ...
    }

//也可以用 array 的方式表示
var month = 5
var MonthInChi = ['一月','二月','三月'...]
console.log(MonthInChi[month - 1] 
```

### ternary 三元運算子
為了節省 if else 的判斷寫法，可用三元運算子表示方式如下:
```javascript=
console.log(判斷式 ? 'True 回傳A' : 'False 回傳B')
```
```javascript=
var score = 70
console.log(score >= 60 ? (score ===100 ? 'no1' :　'pass') : 'fail') //也可以用巢狀表示法來寫，但不易讀所以不推薦
```

###### tags: `week2`


