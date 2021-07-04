### 套件簡介
可以快速部屬前後端的環境，並且包含 CI/CD，testing 等
後端主要是 java 或 nest

### creat default project
`npm install -g generator-jhipster` 下載 npm module
`jhipster` 接著在指定的 project 資料夾執行，會詢問一連串建置環境的問題，接著完成基本環境建置

### 資料結構
#### Backend
java - `src/main/java`
Unit / integration test - `src/test/java`
Gatling test - `src/test/gatling`

#### Frontend
`src/main/webapp`


### 運行 app
`mvnw.cmd` or `mvnw.cmd` 快速部屬 maven 環境
(但在目前電腦不能用，待解決)

### security 
default, jhipster 有四種不同的 user profiles
- system
- anonymousUser
- user
- admin