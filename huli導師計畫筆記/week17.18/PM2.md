### Intro
> PM2 is a daemon process manager that will help you manage and keep your application online.
### install
``npm install pm2@latest -g``
### basic command
``pm2 start appName / id``
``pm2 restart appName / id``
``pm2 stop appName / id``
``pm2 delete appName / id``
``pm2 reload appName / id``
``pm2 list / ls /status``
``--watch`` 檔案變更自動重啟
``--max-memory-restart`` 超過記憶體容量時自動重啟
### reference
[pm2 official](https://pm2.keymetrics.io/docs/usage/quick-start/)
[utbuntu 設定 npm global ](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally)
