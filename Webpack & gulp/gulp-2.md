### 環境建置
``mkdir gulp_test`` 建立新資料夾
``npm init -y`` node 環境建置
``npm install --global gulp-cli`` 安裝 gulp-cli
``npm install --save-dev gulp`` 安裝gulp
``touch gulpfile.js`` 建立設定檔
```js
function defaultTask(cb) {
  // place code for your default task here
  cb();
}
exports.default = defaultTask
```
``mkdir src`` 建立來源資料夾
``mkdir dist`` 建立目的地資料夾

### 基本指令
- ``gulp taskname`` 執行任務，預設 ``gulp`` 會執行 default
- 建立任務
```js
gulp.task("taskname", () => {
	...
})

```
```js
function clean(cb) {
  // body omitted
  cb();
}
exports.clean = clean
```
- series() : 可以按照序列執行任務
```js
const { series } = require('gulp');

function transpile(cb) {
  // body omitted
  cb();
}

function bundle(cb) {
  // body omitted
  cb();
}

exports.build = series(transpile, bundle);
```
- parallel() : 可以並列執行
- src() : 指定來源檔案及資料夾，前面會加上 return 
- dest() : 指定目的檔案及資料夾
- pipe() : 執行
```js
const { src, dest } = require('gulp');
const babel = require('gulp-babel');

exports.default = function() {
  return src('src/*.js')
    .pipe(babel())
    .pipe(dest('output/'));
}
```

### 常用套件
- gulp-sass
``npm install node-sass gulp-sass --save-dev``
- gulp-babel
- 