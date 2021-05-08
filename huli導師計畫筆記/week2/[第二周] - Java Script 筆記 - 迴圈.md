# [第二周] - Java Script 筆記 - 迴圈

### label / go to
```javascript=
label:
console.log(i)
i++
if(i<=100){
    goto label
}
console.log('i',i)
```

### 迴圈 - do while
- do while 語法示範_第一種寫法
```javascript=
var i = 1
do{
    console.log(i)
    i++
}
while(i<=10)
console.log('i=',i)

1. var i = 1
2. console.log(1)
3. i = 2
4. while i <= 10
5. conwole.log(2)
6. i = 3
7. while i <= 10
...

```

- 第二種寫法(加入 break)
```javascript=
var i = 1
do{
    console.log(i)
    i++
    if(i >=100 )
    break // 停止迴圈並跳出
}
    while(true)
console.log('i=',i)
```

- 加入 continue
```javascript=
var i = 1
do{
    console.log(i)
    i++
        if(i%2===1)
        {continue //會跳過下一行直接迴圈
        }
        console.log('i=',i)
} while(i<=100)
```
- 用 browser 來執行迴圈
可以比較視覺化的看出執行步驟。
```javascript=
<script>
debugger
var i = 1
do{
    console.log(i)
    i++
} while(i<10)
</script>
```
- 單獨用 while 迴圈跑剛剛的程式，
```javascript=
var i = 1
while (i<100)
{
console.log(i += 1)
}
console.log('i=',i)
```

- 迴圈 for loop 基本語法
```javascript=
for (初始條件 ; 終止條件 ; 每一圈做的事)
```

- 與 while 的語法比較
```javascript=
var i = 1 //初始條件
while(i<10){ //終止條件
    console.log(i)
    i++ //每圈要做的事
}
```

###### tags: `week2`