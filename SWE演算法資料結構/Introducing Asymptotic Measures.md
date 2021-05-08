# Time and Space
## intro duction to Asymptotic measures

### Measures
- Asymptotic analysis 漸進分析
- 保持持續討論的態度，asymptotic analysis 是討論不同解法彼此之間的 trade off，所以其實沒有一個完全正確的解法，重點在於不同解法之間的優劣。
---
來看個例子
```js
int example(int n) {
	for(int i=0; i<10; i++) {
		//do O(1) work
	}
}
```
在這個例子中，不管 n 如何改變 ...`n=1000`、`n=100000000`，結果都會保持 constant，所以他的曲線或者 paramater 就會像是 O(1)

<img width="300px" height="300px" src="https://i.imgur.com/KdyjYI5.png" >

接下來來看一些 O(n) 的例子
```js
int example(int n) {
	for(int i=0; i<n; i++) {
		//do O(1) work
	}
}
```

```js
int example(int n) {
	for(int i=0; i<2n; i++) {
		//do O(1) work
	}
}
```
上面兩個例子，可以清楚的看出來當 n 變大時，會影響運行的次數，呈現 linear 的 parameter，而且第二個例子的斜率更大，但我們其實比較看重不同 parameter 的變化模式，所以可以都簡略為 O(n)。

# Asymptotic Bounding 101
### 如何判斷好壞
- 通常要判斷一個演算法，我們可能會分為 best 、 average、worst
- 下面會可以用一些指標來表達多好、多壞、範圍等
> O() -> bigO //Upper bound，越高，演算法越沒效率
> o() -> little o
> Θ( ) -> theta //exact bound
> Ω( ) -> big omega //越高，演算法越有效率
> ω( ) -> little omega

### 更深入的談 asymptotic bounding
來看一段關於 asymptotic 的數學演示，展示如何逼近 upper bound
> T(n)
> is O(f(n)) "if"
> T(n) <= C*O(f(n))
> for all n>= n

接下來我們假若把 T(n) 的曲線畫出來，然後試試用 O(n)、O(n2)、log(n) 來逼近，會發現只有 linear 的 O(n) 可以無窮逼近 T(n)，所以這時候我們就不會在意 C (constant) 是如何變化，因為只有在選對 "模式" 的狀態下，才能逼近正確的 T(n)

<img width="300px" src="https://i.imgur.com/vmSulrw.jpg">

---
## O(1) Time “Constant Time”
constant(常數)對於一個 function 來說，不影響其"scale"的模式，舉下列例子來說。
- arithmetic operation
```c=
int example(int n) {
  return 1+1
}
```
- Array access
```c=
int example(int[] arr) {
  return arr[0]
}
```
- assignment
```c=
int example(int[] arr) {
  arr[0] = 1
}
```
- Object access
```c=
int example(some object obj) {
  return obj.count
}
```
- boolean comparison
```c=
boolean example(int a, int b) {
	return a < b
}
```
- array insertion
```c=
int example(List<integer>list) {
  return list.add(0)
}
```
---
## O(n) "Linear Time"
### 心態建立
- 不要只瀏覽過 code ，就猜 big(O)，因為通常會問為什麼?

### multilinear bounds
- 通常會出現在 n*n metirx

> O(n) //linear
> O(m+n) //multi-linear
> O(max(m, n))
> O(min(m, n))
- 推導過程
1. max(m, n) <= m+n
2. O(m+n)
3. m+n <= 2*max(m, n)
4. O(max(m, n))

### nested & interdependent Operations
#### 基本觀念
- 盡量省時間，花空間沒關係
```js
for() {
	for() {
	}
}
```

#### array 例子
- 盡量不要在原有的 array 另外拆分獲新建一個 array
- 有效利用 pointer
- 題目
```js
[90, 20, 31, 56, 44, 39, 10] 
把上面的 array 整理成偶數在左，奇數在右。
```
這時我們可以在 array 左邊設置一個 pointer，右邊設置一個 placement pointer，依序比對 pointer 對到的數字是否符合規則，如果不符合就對調，當 pointer 重合時就達到題目的要求了。

#### reference
---
## memorization
#### 關鍵字
- branching factor 分支因子
每隔節點下的子節點數

透過 cache 可以讓原本可能要花 O(n2) 的 algorithm 可以簡化成 O(n)。
原理是透過 cache 幫助我們記憶已經知道的結果

#### 經典的 fibonachi 案例
原始解法
```js
	function fibo(n) {
		if(n<2) {
			return 1
		} else {
			return fibo(n-1) + fibo(n-2)
		}
	}
```
透過 cache 我們可以先把計算過的 fibo(n) cache 起來，節省運算時間
```js
	function fiboMemo(n, cache=[]) {
		if(cache[n]) {
			return cache[n]
		} else {
			if(n < 2) {
				cache[n] = 1
			} else {
				fiboMemo[n] = fiboMemo(n-1, cache) + fiboMemo(n-2, cache)
			}
			return cache[n]
		}
	}

```

[# [\[演算法\] Fibonacci：善用 cache 和 Memoization 提升程式效能](https://pjchender.blogspot.com/2017/09/fibonacci-cache-memoization.html)](https://pjchender.blogspot.com/2017/09/fibonacci-cache-memoization.html)
