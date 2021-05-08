# gulp
### 一個用來處理事件流程的 module
### 設置環境:
1. npm init
2. gulp init

### 常用的 plugin
- gulp-babel : for compile
- gulp-sass : for sass transfer
- gulp-clean-css : for css lighten
- gulp-uglify : for js lighten
> plugin 要先 --save-dev 安裝後，再在 filegulp.js 裡面引入
``const name = require('pluginname') ``才能使用

### 使用方式
就是在 cml 輸入 ``gulp`` 會執行 defaultTASK，如果要執行個別任務，要在 gulpfile.js 用 ``exports.name = functionname`` 並在 cli 輸入 ``gulp name`` 來執行



###### tags: `week13` `gulp`