### | multiple root query
![](Pasted%20image%2020210607004215.png)
#### 原因
原本應該是因為一個 file 裡面有兩個不同 query 會噴錯，但後來發現跟 terminal 進入 file path 的方式有關，如果是用 `cd C/desktop/...` 的這種完整路徑方式的話就可以解決。[解法參考](https://github.com/gatsbyjs/gatsby/issues/19863)