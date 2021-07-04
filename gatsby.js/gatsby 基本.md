### 技術
html、css、JavaScript、React、GraphQL

### 環境建置
install node
install git
`npm install -g gatsby-cli`

### basic command
`gatsby develop` 在 local 執行 project
`gatsby build` 打包 gatsby project
`gatsby clean` 會清除 cashe 和 public directory
`gatsby --help`
`gatsby -v` 查看版本

### 建立新專案
`gatsby new app-name module-url` 建立新專案
`gatsby develop` 執行 dev 模式並跑在 8000 port 上面
`gatsby develop -p port` 執行 dev 並跑在指定的 port 上面

### 專案架構
```js
-- /.cache //gatsby 自動創建的快取
-- /node_modules
-- /public //原始碼編譯後的檔案
-- /src //原始碼，放置元件、模板等
-- /.prettierignore //設置不被 prettier 的 file
-- /.prettierrc
-- /.gatsby-config.js //可以做基礎設定或引入 plugging，含 meta、proxy、mappging
-- /.package.json
-- /.package-lock.json
-- /.README.md
```

### 建立一個新的 page
`cd /src/pages` 進入 src/pages directory
`vim about.js` 建立一個新的 .js file
```js
import React from "react"

export default function About() {
	return (...)
}
```

### router
```js
import Link from "gatsby"

function router() {
	return <Link to="./path">link</Lin>
}
```

### deploy
- getsby cloud 
getsby depoly platform(build / deploy / host)，free for personal user
檔案會放在 git 上面，
`gatsby build`

### styling
#### gatsby-browser.js
`gatsby-browser.js` 會放在主資料夾內，裡面可以 import `.css` file ，來設定一些共同的 styling
```js
gatsby-browser.js
src -- styles -- global.css
```
```
//gatsby-browser.js
import "./src/styles/global.css"
```

#### style.module.css
另一種是針對特定 component 可以設定專用的 css.module，gatsby 會自動辨認 `.module.css` 檔名，並轉換 css 內容為特定代碼，避免混用
```js
--src -- styles -- footer.module.css
      -- components -- footer.js
```
`import * as footerStyle from "../styles/footer.module.css"`

### graphQL
#### use pagequery
- 首先要在 `gatsby-config.js` 檔案裡面設定 `siteMetadata` 方便在 page 裡面提取
```js
module.export = {
	siteMetadata: {
		key: value,
	}
}
```
- 接著在 page 裡面透過引入 `graphql` 來 query
```js
export function page({data}){ // 這邊要傳入 query data
	const query = graphql`
		query {
			site {
				siteMetadata {
					key
				}
			}
		}
	`
}
```

#### graphiQL
- gatsby 引用 data 的方式可以用 API、database、CMS、localfiles 等
- graphiQL 是一種 in-browser 的 IDE 管理工具
- 可以透過在 browser 輸入 `http://localhost:8000/___graphql` 來使用
- graphiQL 會自動產生 query 的 SQL 語法，可以使用在 page、component 中

#### gatsby-source-filesystem plugin
- 可以用來獲取 database file data
- `npm install gatsby-source-filesystem` install
- 接著在 graphiQL 會看到多出 `file` `allFile` 的欄位
![](https://www.gatsbyjs.com/static/88ec3efe94e380d32bc1a20cd82dd8bf/373fb/graphiql-filesystem.png)


#### useStaticQuery
針對非 page 的 query 也有對應的 hook 可以用，用法類似 graphql 但不用傳入 data(這邊待釐清)
```js
import {useStaticQuery, graphql} from "gatsby"
const data = useStaticQuery(graphql`
	query {
		site {
			siteMetadata {
				key
			}
		}
	}
`)
```

### plugging
- [gatsby 社群](https://www.gatsbyjs.com/plugins)
#### [typography.js](https://kyleamathews.github.io/typography.js/)
可以透過引入 style module 的方式來進行 styling，需要在 `src/utils` 裡面建立 `typography.js` 檔案
`npm install --save gatsby-plugin-typography react-typography typography typography-theme-fairy-gates
`
[npm](https://www.npmjs.com/package/gatsby-plugin-typography)

#### gatsby-transfrom-remark
- transformer plugin，可以用來轉換 md 等檔案為 html 檔
- `npm install gatsby-transformer-remark`
- 接著會在 graphiQL 裡面看到新增了 `allMarkdownRemark` `MarkdownRemark` 等欄位



### refer
[gatsby 鐵人賽](https://ithelp.ithome.com.tw/articles/10239465)