### ORM
> Object-Relational Mapping (ORM, O/RM, or O/R mapping)一詞就是將關聯式資料庫映射至物件導向的資料抽象化技術。
- 優點: 
1. 防止 sql injection
2. 避免大量撰寫 sql 及重複的程式碼
3. 方便轉移資料庫
- 缺點:
1. 犧牲性能
2. 複雜查詢比不上直接撰寫 sql

### Sequelize
- Installing
``npm install --save sequelize``
``npm install --save mysql2``
- Setting up a connection
- Testing the connection
- Modeling a table
因為 orm 是把 table 當作一個物件，所以可以針對物件做相關設定，詳情查 ``Model definition``
- Synchronizing the model with the database
自動創建 table
- query
透過 sequelize 的 query 指令可以進行各式 php 指令，請查閱 official query 篇章
```js
Project.findByPk(123).then(project => {
})

Project.findOne({
  where: {title: 'aProject'},
  attributes: ['id', ['name', 'title']]
}).then(project => {
})
```
- Assosiation 關聯
在 php 裡面要透過 join 指令來關聯，但 sequelize 則是靠另外一種方式，透過指定單向關係，來界定不同 table / model 的連動關係，當關係被建立的時候，相對應的 table 會新增一個 "userId" 欄位，來指認對應的 table 內的相對項目，當該項目被刪除時會顯示 null ，變動時也會一併更新
- foreign key 外鍵
> 外鍵是一個 (或多個) 指向其它資料表中主鍵的欄位，它限制欄位值只能來自另一個資料表的主鍵欄位，用來確定資料的參考完整性 (Referential Integrity)。
- relation / association
> ``hasOne`` : 1 - 1 relation ，會在 target 建立 association key，例如 ``player hasOne(team)`` 那就會在 team 建立 key

> ``belongsTo`` 1 -1 relation，會在 source 建立 association key

> ``hasMany``: 1 - many relation
> ``belongsToMany`` : 1 - many relation

- 手動添加 association
注意如果要添加 asscition 用 addColumn 的方式出現 ``Can't create table `w17_bite`.`lotteryimgs` (errno: 150 "Foreign key cons
traint is incorrectly formed")`` 錯誤的話可以用下列偵錯
1. 確認 foreinkey 跟 reference key 的 datatype 設定有沒有一致
2. 確認 engine 都是 innoDB
3.  如果 reference key 不是 primary key 的話要設定 index 給該欄位``ALTER TABLE table_name ADD INDEX (column_name)``

### sequelize CLI
- init
``npm install --save-dev sequelize-cli``
``npx sequelize-cli init`` or
``./node_modules/.bin/sequelize ini``
資料夾內就會建立 config / models / migrations / seeders 等四個子資料夾
- config 
可以透過 config.json 來設定不同環境的連線設定
- models
`` npx sequelize-cli model:generate --name User --attributes firstName:string,lastName:string,email:string``
會產生一個 model 及 migration 檔，這時候都還只是設定檔，尚未執行真的資料庫建置
- migration
``npx sequelize-cli db:migrate``
> 1. up: 下一步要執行的步驟 
> 2. down: 上一動
- undoing migration
會把原本 migration 建立的 db 給清除掉
``npx sequelize-cli db:migrate:undo``
``npx sequelize-cli db:migrate:undo --name 20180704124934-create-branch.js``

- seeders 種子資料
當我們利用 ``sequelize:migrate`` 來建立資料之後，可能會想建立一些 default 資料，這時候可以
1. 輸入 ``npx sequelize-cli seed:generate --name default-admin-user`` 建立如 ``xxx-default-admin-user.js``  的 seed file
2. 接著在 file 裡面增加要新增的資料(up/down)如
```js
'use strict';
module.exports \= {
up: (queryInterface, Sequelize) \=> {
return queryInterface.bulkInsert('Users', \[{
name: 'admin',
email: 'admin@demo.com',
password: 'password',
sex: 'male',
createdAt: new Date(),
updatedAt: new Date()
}\], {});
},
down: (queryInterface, Sequelize) \=> {
return queryInterface.bulkDelete('Users', null, {});
}
};
```
3. 接著輸入 ``npx sequelize-cli db:seed:all`` ，就會產生新的一筆資料



### basic command


### reference
[Sequelize](https://sequelize.org)
[sequelize relations](https://sequelize.readthedocs.io/en/latest/docs/associations/)
[res.redirect / res.location]((https://codertw.com/前端開發/241450/))


