# [第三周] - [MTR04] - eslint 設定
### eslint = es + ling 
> es = ECMAScript 
> lint 程式碼檢查

### 先看看 huli 安裝的 eslint
1. 透過 mentor-program-4th-ianchen6501 clone 到本地
2. 在 clone 完的資料夾裡面 'npm init'
3. 就可以在 node_modules/  package.json  package-lock.json 看到有 eslint
4. 另外在 init 的過程中會看到 git hook 表示之後執行的時候都會一併執行 hook 的流程(檢測)
![](https://i.imgur.com/o01VU4H.png)

### 執行 eslint
- 在有安裝 eslint 的資料夾內新增一 js 檔案並隨便寫一段 code ，之後在 commit 的時候會自動執行 eslint 檢查
- 執行完如果有錯誤， eslint 會逐條列出錯誤，要全部解決才可以成功 commit 
- 錯誤的範例說明如下: 
"1:10  error  'add' is defined but never used                   no-unused-vars"
表示第1行第10個字有錯， add 這個 function 從來沒有執行過， 如果不知道錯誤內容可以 google "no-unused-vars"
![](https://i.imgur.com/G3yeMVq.png)
### eslint disable
- 如果某些錯誤無法避免要 disable 那就在 code 的第一行加入下列程式碼，之後再 commit 應該就可以 disable 那個錯誤
```javascript=
/*eslint-diable no-unused-vars*/
```
- 另外一個方式是在要 disable 的那一行加入下列程式碼
```javascript=
/* eslint-disable-next-lime */
```

### 注意事項
- warning 不用修正
- 推薦從後往前修正錯誤，避免一開始就修改行號打亂順序，要重新 commit 

###### tags: `week3`

