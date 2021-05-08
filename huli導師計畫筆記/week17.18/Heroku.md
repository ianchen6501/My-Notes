### Intro
提供各種不同服務，這次要利用 heroku 來部屬網站

### environment variable 環境變數
為了安全問題，不會將某些資訊寫在 code 裡，所以可以用設定環境變數的方式，在執行時帶入變數，環境變數會儲存在主機裡面。
1. ``process.env.env_name`` 在 code 裡面先預設 env
2. 接著透過下列兩種方式就可以在 terminal 設定環境變數，
``env_name='' node app_name`` 
``export env_name=''`` 
3. 要查詢環境變數可以用 ``echo $env_name`` ，前面加上 $ 的方式

### deploy 部屬
1. set package.json - start and engine
``"start": "npm run db:migrate && node index.js",``
``"db:migrate": "npx sequelize-cli db:migrate"``
``"engines": { "node": "12.18.1", "npm": "6.14.5"},``
2. set config
``"use_env_variable": "CLEARDB_DATABASE_URL"``
4. set index.js port
``const port = process.env.PORT || 5004``
5. heroku login
6. heroku create
7. create clear db (set )
``heroku addons:create cleardb:ignite``
9. git push

### basic command
``heroku ps:scale web=1`` set dyno number











