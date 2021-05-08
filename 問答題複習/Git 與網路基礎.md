P1 你說得出程式如何執行
> 程式是一行一行執行，編碼者怎麼制定規則與流程，程式就怎麼執行。

P1 你理解寫程式的本質只是一行行的指令
> 是。

P1 你了解前端與後端的區別
> 前端: 負責所有與 client-side 接觸到的介面，包含 UI、網路畫面、使用者互動ㄉ等。前端就像餐廳的前台，負責使用者點餐的需求並交給後端處理。
> 後端: 負責處理與提供前端所需要的資料，後端主要負責伺服器與資料庫的管理。當前端發送 request 過來的時候，後端要根據需求做出回應。後端就像餐廳的後台，接到訂單後就負責料理，完成後就交給前端送給客人。
 
P1 你能說出從發出一個 request 到接收 response 中間發生的事
使用者發出 request 的流程
> 使用者 -> 瀏覽器 -> 作業系統 -> 網卡 -> request -> DNS(會回傳目標 IP 給使用者) -> 目標伺服器(有需要拿取資料就發 request 給資料庫，不需要就回傳 response) -> 發出 respose
> 伺服器 -> response -> 使用者

P1 你了解不同載具的差異在哪（Desktop、Mobile、Web
> 不同載具不同點在於畫面尺寸不同，需要作出相應的 RWD 設計，另外不同載具可能會有不同的瀏覽器，瀏覽器針對 html tag 或 js語法(ES6)及相關 module 也會有不同的相容性。
 
P1 你了解基本的 command line 指令
> mv、touch、mkdir、rmdir、cd、ls

P1 你知道 Git 在做什麼，以及為何我們需要 Git
> Git 主要在做檔案的備份與版本控制，因為檔案的儲存如果分很多不同資料夾管理不易，而且資料容易丟失，Git 可以幫助我們記錄不同開發版次的內容，也可以同時開不同分支來開發不同功能。
 
 P1 你知道 add、commit、push、pull 等基本 Git 指令
 > add 提交並加入索引
 > commit 建立版本
 > push 上傳 github
 > pull 與 github 同步
 > log 查看版本資料
 > status 查看當前版本狀態與索引檔案
 
 P1 你知道怎麼使用 branch 並送出 Pull Request
 > git branch branchname 建立新的 branch
 > git branch -d branchname 刪除 branch
 > git branch -v 查看 branch
 > git push remote branchname 推送並至 github 發出 pull request
 
 P2 你熟悉 Git Workflow（其實就是交作業的流程）
 > 開發新功能時依照下列步驟
 > 1. git branch branchname 開新的 branch
 2. git add .
 2. git commit -am "commit name"
 3. git push remote branchname
 4. pull request
 5. 確認後 merge pull request
 6. git pull remote branchname
 7. git branch -d branchname