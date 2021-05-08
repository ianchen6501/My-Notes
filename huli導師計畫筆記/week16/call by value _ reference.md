# call by value / reference
### call by value
在 javaScript 裡面，假若在一個函式裡面我們要引用或引入一個變數，其實我們是在另外一個記憶體位置，建立一個原變數值的複製，如下面例子，原本預計 x, y 的值會對調，但執行完後卻會發現沒有產生預計的效果，這原因就是除了 object 已為，像 x, y 這種 primitive type 我們在 function 裡面其實是建立了一個 x,y 的複製值 a, b 儲存在另外的記憶體位置中，所以在 swap function 中總共建立了 temp, a, b 另外三個記憶體位置，而原本的 x, y 就沒有被更改到，這就是 call by value (pass by value) 的意義。
```javascript=
function swap(a, b) {
  var temp = a;
  a = b;
  b = temp;
}
  
var x = 10;
var y = 20;
swap(x, y);
console.log(x, y) // 10, 20
```
如果我們想要達到 swap 的效果，其實我們應該要在 a, b 放入一個值指向 x, y 的記憶體位置，所以利用這種指標的方式我們可以在函式裡面改到 a, b 的值(在 c 語言裡面)
```javascript=
void swap(int *a, int *b) {
  // 印出 a 跟 b 所存的值
  printf("%ld, %ld", a, b); //0x44, 0x40
  int temp = *b;
  *b = *a;
  *a = temp;
}
  
int main(){
  int x = 10;
  int y = 20;
  // 印出 x 跟 y 的記憶體位置
  printf("%ld %ld\n", &x, &y); // 0x44, 0x40
  swap(&x, &y); // 傳記憶體位置進去
  printf("%d %d\n", x, y); // 20, 10
}
```
### call by reference
但如果我們把上面的 x, y 改成傳入 object ，會發現不一樣的結果。
```javascript=
function add(obj) {
  obj.number = obj.number + 1
}
  
var o = {number: 10}
add(o)
console.log(o.number) // 11
```
這個時候其實我們可以看成是改到同一個記憶體位置 obj 裡面的值，所以可以展生預期的效果(call by reference)，但在看看另一個例子
```javascript=
function add(obj) {
  obj = {
    number: obj.number + 1
  }
}
  
var o = {number: 10}
add(o)
console.log(o.number) // 10
```
在 add function 中，我們其實創建了一個新的 obj 在新的記憶體位置，所以原本的 o 其實不會被改變。所以上面的那個可以透過引數來改變外部變數的我們就另外稱為 call by sharing

[深入探討 JavaScript 中的參數傳遞：call by value 還是 reference？](https://blog.huli.tw/2018/06/23/javascript-call-by-value-or-reference/)
###### tags: `week16` `call by value`