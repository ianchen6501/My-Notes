### 基本簡介
- TypeScript 是基於 JavaScript 加上強大的型別系統，需要轉譯成 .js 才能使用，所以需要 tsc / gulp module 來轉譯
- 因為 TypeScript 簡化了 JavaScript，也包含物件導向的概念，因此也提高了程式碼的可讀性和可維護性
- TypeScript 會進行型別的檢查，幫助我們在開發時就抓出錯誤並提示，有別於以往 JavaScript 需要運行才能發現錯誤
- TypeScript 是開源的
- 完全相容 JavaScript 語法，可循序漸進的學習


### 套件
#### typeScript
typeScript `npm install typeScript -g`


#### ts-node (可以看成 node.js + TSC)
可以直接運行 ts 檔
`npm install ts-node`
`tsc --init` 初始化 tsconfig.json
`npx ts-node index.ts` 或用 npx 直接運行
`tsc index.ts` 會將 index.ts 轉譯成 .js 檔
`tsc index.ts --noEmitOnError` 如果有錯會報錯並停止轉譯
`ts-node index.js` 轉譯後並執行 node.js

### 基礎語法
#### Type Annotation
`function foo(name : string)`

#### interface
建立一個物件中屬性的 type 定義雛形，之後可以將 interface 當作一種自定義的 types 來使用。
注意 interface 不需要加 `,` 分隔
```ts
interface Car {
  type: string
  number: number
  isSold: boolean
	note?: string //加問號代表可有可無
}

const car1 : Car =  {
  type: "ignis",
  number: 1,
  isSold: true
}

const car2 : Car =  {
  type: "kiks",
  number: 3,
  isSold: false
}
```

### reference 
[TypeScript 10分鐘快速入門](https://eddychang.me/typescript-quick-start-in-10-mins)