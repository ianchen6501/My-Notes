## | 基礎語法

#### res.send()

會回傳 HTTP response，並依據回傳的內容決定 Content-Type

- 語法:

```js
res.send(Buffer.from("whoop")); //Content-type _ application/octet-stream
res.send({ some: "json" }); //Content-type _ JSON
res.send("<p>some html</p>"); //Content-type _ text
res.status(404).send("Sorry, we cannot find that!");
res.status(500).send({ error: "something blew up" });
```

#### res.json()

會回傳 json 格式的 HTTP response。

- 語法:

```js
res.json(null);
res.json({ user: "tobi" });
res.json("result");
```

#### res.end()

會結束 response 的流程

- 語法:

```js
res.end(); //注意 res.end() 裡面盡量不要回傳 response
res.status(404).end();
```

#### res.query()

- url:
  `myWebsite?id=xxx`
- 語法:

```js
req.query.id(); //xxx
```

#### res.params()

取得網址列的參數

- url:
  `myWebsite/:paramsName`
- 語法:

```js
req.params.paramsName();
```

---

### | 關於 cookies / sessions

#### 設置 cookie

`res.cookie(name, value [, options])`

- cookie 是 name-value 的結構，並且要注意 value 只能存 string 或 json。
- options 可以設定不同 cookie 屬性。

| 項目     | Type             | 說明                                                                                                                       |
| -------- | ---------------- | -------------------------------------------------------------------------------------------------------------------------- |
| domain   | String           | cookie 的 domain name。                                                                                                    |
| encode   | Function         | 同步的幫 value 編碼，預設為 encodeURIComponent，也可以改為 String 那 value 就不會進行另外編碼。                            |
| expires  | Date             | 設定到期時間(GMT)，未設定或設為 0 就會變成 session cookie 的形式                                                           |
| httpOnly | Boolean          | 限制 cookie 只能被 web server 存取，禁止其他使用者以 JavaScript 的方式存取，避免 XSS 攻擊                                  |
| maxAge   | Number           | 設定 cookie 的存續時間，單位為毫秒。                                                                                       |
| path     | String           | 適用該 cookie 的路徑，預設為"/"。                                                                                          |
| secure   | Boolean          | 設定此 cookie 是否只能在 https 中使用。                                                                                    |
| signed   | Boolean          | 設定此 cookie 是否需要進行簽屬，避免使用者偽造 cookie。                                                                    |
| sameSite | Boolean / String | 可以設定為 Strict / Lax / none (要搭配 secure = true)。主要是 browser 為了防止 csrf 的攻擊，目前 chrome 瀏覽器預設為 Lax。 |

> 補充一下 sameSite，之前自己只聽過 sameOrigin，其中 origin 是由 schema + host + port 組成。而 site 則是 eTLD +1 ， eTLD(有效頂級域名, effective top-level domain)，就是 mozilla 維護的 public suffix 如 `.com`、`.org` 等，那 eTLD+1 就是
> 像 `google.com` 等。所以說 site 其實是不管 schema + port 的。

> 這邊想談一下如果在 server 設定 cookie，常會發現設定都沒問題，response set-cookie header 也有跑出來，但瀏覽器怎麼就是不會存 cookie 的狀況。

### 讀取 cookie

讀取未署名 cookie
`console.log(req.cookies.cookieName)`
讀取署名 cookie
`console.log(req.signedCookies.cookiename)`

### 刪除 cookie

```js
res.cookie("test", { path: "/test" });
res.clearCookie("test", { path: "/test" });
```

---

### reference

[網站安全 🔒 再探同源政策，談 SameSite 設定對 Cookie 的影響與注意事項](https://medium.com/程式猿吃香蕉/再探同源政策-談-samesite-設定對-cookie-的影響與注意事項-6195d10d4441)
[Day24 - Cookie 在 express 上的應用—登入實作為例。](https://ithelp.ithome.com.tw/articles/10187343)
[CORS 完全手冊（三）：CORS 詳解](https://blog.huli.tw/2021/02/19/cors-guide-3/)
[Day 26 - Cookies - SameSite Attribute](https://ithelp.ithome.com.tw/articles/10251288)
