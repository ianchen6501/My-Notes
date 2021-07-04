# 物件導向 Object-oriented Programing (OOP)
### 物件導向基本性質
- after ES6
- 每建構一個新的 instance ，要用 new

### 名詞解釋
Object：
> An object is characterized by a number of operations and a state which remembers the effect of these operations.

Class
> A class represents a template for several objects and describes how these objects are structured internally. Objects of the same class have the same definition both for their operations and for their information structures.

Instance
> An instanceis an object created from a class. The class describes the (behavior and information)structure of the instance, while the current state of the instance is defined by the operations performed on the instance.

基本上 class 就是一個模板、類型、族類，下面可以產生不同的 object / instance ，object 跟 instance 可以視作同一個東西，只是如果要單指某個特定的物件，會用 object ，如果是指大的概念會用 instace ，所以我們可以說 ``a.b object is belong to the same instance.``

### 基礎範例
下面用一個基礎範例，來示範 class 建立，getter / setter / constructor 的使用方式
```javascript=
//物件導向 OOP ，ES6
class human {
  //建構子
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  sayhello() {
    console.log(this.name, this.age)
  }
  //setter
  setNickname(name) {
    this.nickname = name
  }
  //getter
  getNickname() {
    return this.nickname
  }
}
//範例
var ian = new human //創建一個新的 object
ian.sayhello() //使用 ian 的 operation(動作)
ian.setNickname('小明') //設定 ian 的 data
console.log(ian.getNickname())
ian.nickname = '小田的男友' //object 的 property 可以透過這樣的方式修改，但不建議
console.log(ian.nickname)

//透過 constructor 新建物件
var emily = new human('emily', 23) //用餐數回傳建立新的 object
emily.sayhello()

var ivy = new human('ivy')
ivy.sayhello()
```
但雖然說物件導向(OOP)的寫法是在 ES6 之後才出現的，卻不代表 ES5 是無法達到同樣的效果，下面我們用另一個例子重新寫一個 ES5 版的物件導向範例
```javascript=
function human(name) {
  var myName = name
  return {
    sayhello : function() {
      console.log('hello')
    },
    getName : function() {
      return myName
    },
  }
}

var ian = human('ian')
ian.sayhello()
console.log(ian.getName())

var emily = human('emily')
emily.sayhello()

console.log(ian.sayhello === emily.sayhello) 
//儲存的記憶體位置不一樣，會耗費記憶體
//所以其實 ES5 也是有保留部分 new 的寫法，用 new 的時候 function 就可以當 class 使用
function dog(name) {
  this.name = name
}
dog.prototype.getName = function() { //用 .prototype.functionName 可以設定 operation
  return this.name
}
dog.prototype.setNickname = function(nickname) {
  this.setNickname = nickname
}
dog.prototype.sayHello = function() {
  console.log('hello')
}

var d = new dog('wowo')
console.log(d.getName())

var b = new dog('hehe')
console.log(b.getName())

console.log(b.sayHello === d.sayHello) //這時候儲存的記憶體位置就相同
```
### 原型鍊 prototypeChain
上面大致示範了 OOP 的簡單應用，但如果要更理解 OOP 的 object 是怎麼知道 class 的屬性的，就必須要理解"原型鍊 prototypeChain"，原型鍊可以看成一種母子關係的表示，
```javascript=
function dog(name) {
  ...
}
var a = new dog()
a.__proto__ = dog.prototype //true
```
上面我們可以看到用 ``.__proto`` 和 ``.prototype`` 可以找到物件的上下層原型鍊關係，甚至我們可以用 ``A.prototepe.operation = function(){}`` 的語法來建立不同的方法。
```javascript=
function dog(name) {
  this.name = name
}
dog.prototype.getName = function() { //用 .prototype.functionName 可以設定 operation
  return this.name
}
dog.prototype.setNickname = function(nickname) {
  this.setNickname = nickname
}

var d = new dog('wowo')
var b = new dog('hehe')
//console.log(b.__proto__) //dog.prototype
//console.log(b.prototype) //undefined

dog.prototype.sayHello = function() {
  console.log('dog', this.name)
}
Object.prototype.sayHello = function() {
  console.log('object', this.name)
}
d.sayHello() //dog d ，因為 prototypeChain 是由內往外找
console.log(d.__proto__ === dog.prototype) // true
console.log(dog.__proto__ === Function.prototype) //true

/*用 prototypeChain 來理解 d 跟 dog 的關係
1. d 的身上有沒有 sayHello()
2. d.__proto__ 有沒有 sayHello()
3. d.__proto__.__proto__ 有沒有 sayHello()
4. d.__proto__.__proto__.__proto__ 有沒有 sayHello()
5. null 到頂了

d.__proto__ = dog.prototype
d.__proto__.__proto__ = Object.prototype
dog.prototype.__proto__ = Object.prototype
*/
```
接著我們來看一些原型鍊的應用範例，可以看到除了 function 創造出來的 class 可以用原型鍊外，甚至各個型別(string / number / object ...)都可以建立 operation。
```javascript=
// __proto__ 與 prototype 應用
var a = '123'
console.log(a.__proto__ === String.prototype)
console.log(a.toString === String.prototype.toString)

//也可以直接對型別加 prototype
String.prototype.first = function() {
  return this[0]
}
console.log(a.first())

Number.prototype.square = function() {
  return this * this
}
var num = 3
console.log(num.__proto__ === Number.prototype)
console.log(num.square())
```
### new
上面我們看到可以用 new 來創建一個 object ，但 new 實際上是做了什麼事，我們可以拆解為幾個步驟。
> 1. 創建一個新的物件
> 2. 把新的物件當作 this 丟進 constructor 中(運用call())
> 3. 建立 this.__proto__ 與 constructor.prototype 的關係
> 4. 把物件丟回來成為一個全域變數

下面我們先看 call() ，是怎麼作用的，基本上 call 可以幫助我們傳入一個 this 值 ``.call(thisarg, arg, arg)`` ，並回傳執行的結果
```javascript=
function test() {
  console.log(this)
}
//call 會回傳 function 執行的結果，這邊要記住 call 回傳的 this 就是我們傳進去的參數
test.call(123) //[number, [123]]
test.call('123') //[string, [123]]
test.call([]) //[]
```
知道了 call 的作用後，就可以來看看上面的四個步驟是怎麼作用的，我們可以試著寫一個 function 出來
```javascript=
//constructor -> 方法
function dog(name) {
  this.name = name
}
dog.prototype.getName = function() {
  return this.name
}
dog.prototype.sayHello = function() {
  console.log('hello')
}
//這邊我們來看 new 到底做了什麼事 -> 指定 this
function newDog(name) {
  var obj = {}                    //1. 建立一個物件
  dog.call(obj, name)             //2. 把物件當作 this 丟進 constructor
  obj.__proto__ = dog.prototype   //3. 設定 proto 及 prototype 的關係
  return obj                      //回傳物件
}
// === var obj = new dog('obj')
```
### 繼承 inheritance
既然我們都可以設定物件了，為了避免重複設定很多類似的物件模板，其實 OOP 還有一個很重要的特性 "繼承 inheritance"，可以讓物件的屬性傳遞下去。要建立繼承，我們可以創建一個新的 class 並用 ``extend`` 指令來達成繼承。
```javascript=
class dog {
  constructor(name) {
    this.name = name
  }
  sayHello() {
    console.log(this.name)
  }
}
//利用 extends 來建立繼承 class
class Blackdog extends dog {
  constructor(name) {
    super(name) //dog 的 constructor，這邊會這樣輸入是為了讓母 class 的 this 初始化及輸入我們指定的參數
    console.log('hello')
  }
  test() {
    console.log('test!', this.name)
  }
}
//這邊我們會觀察到屬性其實會傳遞到子物件中
const d = new Blackdog('hello')
```


### reference
[什麼是物件導向（2）：Object, Class, Instance](http://teddy-chen-tw.blogspot.com/2012/01/2object-class-instance.html)





###### tags: `week16` `物件導向` `OOP` `inheritance` `prototypeChain`