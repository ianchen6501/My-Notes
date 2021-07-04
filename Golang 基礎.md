### 基礎指令
- `go mod init example.com/hello`
作用類似`npm init`，會產生一個`mod.go`file，可以引入外部的 module 或 source code。
- `go run exampleFile.go`
執行 go
- `go help`
可以先用來認識一些基本的 Go 指令

### Hello world
學語言總要先有個最小可行產品，先從 Hello world 開始吧。
1. `mkdir hello`
2. `cd hello`
3. `touch hello.go`
4. `open hello.go`
```js
package main

import "fmt"

func hello(){
	fmt.println("Hello, World!")
}
```

### 引入 module
通常我們會透過`mod init repopath` 的方式引入 module，但這邊在 local 環境可以用另一種作法。
1. 首先建立一個 greeting 的資料夾並 `go mod init example.com/greeting`，這個 module 是預備之後要被引入的部分。
2. `touch greetings.go`
3. `open greetings.go`
```js
package greetings
import "fmt"

func Hello(name string) string { //第一個 string 是傳入的值，第二個 string 是回傳的值
	message := fmt.Sprintf("Hi, %v. Welcome!", name) //%v 會被 name 給取代
	return message
}
```
4. 接著在與 greetings 資料夾同一個層級新建另一個資料夾 `mkdir hello`
5. `cd hello` `touch hello.go` `open hello.go`
```js
package main
import (
 "example.com/greetings"
 "fmt"
)

func main() {
	message := greetings.Hello("Ian")
	fmt.Println(message)
}
```
6. 這時候如果直接執行 `go run hello.go` 會找不到目標 module
7. 所以必須把 `example.com/greeting` 的 path 替換掉 `go mod edit -replace=example.com/greetings=../greetings`
8. 接著執行 `go mod tidy` 讓 go update 相關 module
9. 在進入 `mod.go` 就會發現檔案變成，在執行一次就成功了。
```js
module example.com/hello
go 1.16
replace example.com/greetings => ../greetings
require example.com/greetings v0.0.0-00010101000000-000000000000
```




### reference
下面有幾個不錯的 golang 學習網站
[Golang網頁設計敎學](https://michaelchen.tech/golang-web-programming/#list-pane)

官方教學
[effective go](https://golang.org/doc/effective_go#init)


