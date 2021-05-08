# [第三周] - [MTR04] - NPM 簡介
### Node Package Manager
- package : Node 的套件
- NPM 管理 Node 套件的系統
- 安裝 Node.js 就會一併安裝
```
npm -v //用 gitbash 查詢 npm 版本
6.14.5
```

### NPM 初始化設定
1. 在要執行 NPM 設定的資料夾輸入 'npm init' ，接下來一直按 enter
![](https://i.imgur.com/hw0ehu3.png)
2. 接著會在資料夾新增 package.json 檔案

### 安裝套件，以 math.js 為例
- 可至 google search 'npm math'
- 執行 CLI 'npm install mathjs'
- 跑完就執行完成了 
![](https://i.imgur.com/ltmBJsd.png)
- 接著看資料夾會多出一個 package-lock.json 的檔案，裡面會記錄用到了哪些套件
![](https://i.imgur.com/G20l60x.png)
- 另外也會新增一個 node_modules 的資料夾，裡面會有 mathjs 的安裝資料夾和 mathjs 會用到的其他套件
- 如果要在 package.json 的 dependancy 裡面留下 package 紀錄的話
在 install 時要記得後面加上 '--save' or '--save-dev'
```javascript=
npm install module_name --save
npm install module_name --save-dev //會出現在 package.json 裡面的 'devDependencies'
```

### 共同工作要分享 NPM 時的流程
- 不用把 node_modules 給上傳，只要同事下載 packge.json 及 package-lock.json 再執行 npm init 系統就會自動下載需要的套件

### 執行 math.js
1. 先建立一個 js 檔案
2. 在裡面引入 math.js (node.js)
```javascript=
const { sqrt } = require('mathjs')
console.log(sqrt(-4).toString()) // 2i
```

##### 如果在子資料夾安裝 package ，系統會判斷這是一個大專案， package 會安裝在母資料夾裡的 node_modules 資料夾裡面，而不會在子資料夾另開一個資料夾放套件

##### 如果真的要在子資料夾建立一個 node_modules 必須要重新在該資料夾 npm init 之後在重新 'npm install math.js' 就會安裝在子資料夾裡面的 node_modules 了

###### tags: `week3`

