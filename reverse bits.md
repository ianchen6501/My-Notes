### 程式碼
```js
//轉換為 2 進位

let n \= 123453

let array \= \[\]

while(n) {

 const log2 \= Math.floor(Math.log2(n))

 array.push(log2)

 n \= n \- Math.pow(2, log2)

}

let N \= 0

array.forEach((pow) \=> {

 N += Math.pow(10, pow)

})

//console.log(N)

//翻轉

const NArray \= N.toString().split("")

let reverseN \= 0

//console.log(NArray.length)

for(let i\=NArray.length\-1; i\>=0; i\--) {

 reverseN += Number(NArray\[i\])\*Math.pow(10, i)

}

//console.log(reverseN)

//轉換為 10 進位

let reverseNDec \= 0

let reverseNLog \= parseInt(Math.log10(reverseN))

//console.log(reverseNLog)

for(let i\=0; i<=reverseNLog; i++) {

 if(reverseN % 10 \=== 1) {

 reverseNDec += Math.pow(2, i)

 //console.log(reverseNDec)

 }

 reverseN \= Math.floor(reverseN/10)

}

console.log(reverseNDec)
```