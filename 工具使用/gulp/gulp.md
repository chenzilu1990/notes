
## 安装

> 全局安装

```bash
   npm install gulp -g  
```     

> 到项目根目录下再安装一次，确保你根目录存在package.json文件

```bash
npm install gulp —save-dev
```

> 插件列表

- sass的编译 gulp-ruby-sass
- 自动添加css前缀 gulp-autoprefixer 
- 压缩css gulp-minify-css
- js代码校验 gulp-jshint
- 合并js文件 gulp-concat
- 压缩js代码 gulp-uglify
- 压缩图片 gulp-imagemin
- 自动刷新页面 gulp-livereload
- 图片缓存，只有图片替换了才压缩 gulp-cache
- 更改提醒 gulp-notify
- 清除文件 del

## 使用文档

 > **gulp.src(globs[, options])**
 
 src方法是指定源文件的输入路径，pipe有点像是封闭的“流水线”，某个产品经过上一个工序处理后，就转入下一个工序去处理，直到完成。也就是将上一步的输出转化下一步的输入的中间者。
 语法：
 ```bash
 gulp.src(globs[, options])
 ```
 参数：
 globs
 　　类型：String 或 Array，指定源文件的路径，可以是单个路径，也可以是个路径数组。
 　　路径匹配支持通配符：
 　　　　- app.js　　　　指定具体文件
 　　　　- js/　　　　　匹配 js 目录下所有的文件，不包括子文件夹
 　　　　- js/.js　　　 匹配 js 目录下所有的扩展名为 .js 的文件，不包括子文件夹
 　　　　- js//.js　　匹配 js 目录下第一层子文件夹里的扩展名为 .js 的文件
 　　　　- js/**/*.js　 匹配 js 目录下所有文件夹层次下扩展名为 .js 的文件
 　　　　- !js/try.js　 不包括 try.js 文件，在前五条文件匹配模式前加!，就忽略掉相应的文件
 options
 　　类型：Object，有3个属性buffer，read，base。
 　　　options.butter
 　　　　类型：Boolean，默认：true
 　　　　gulp-api 上描述到，如设置为false，返回的文件内容将会以数据流的形式体现，而不是数据
 　　　　块的形式。还提示到有可能一些插件没有实现支持数据流的形式。
 　　　　(表示不太明白，有待研究。-_-|||)
 　　　options.read
 　　　　类型：Boolean，默认：true
 　　　　返回的文件内容为null，不执行读取文件操作。
 　　　options.base
 　　　　类型：String
 　　　　设置输出路径以某个路径的某个组成部分为基础向后拼接。具体例子可以参考 gulp-api。
 
 > **gulp.dest(path[, options])**
 
 dest方法是指定被处理完的文件的输出路径。
 
 语法：
 ```bash
 gulp.dest(path[, options])
 ```
 参数：
 
 path
 　　类型：String 或 Function，指定输出文件的文件夹路径，可以是字符串，也可以是一个返回文件夹路径的函数。
 options
 　　类型：Object，有2个属性cwd，mode。
 　　　options.cwd
 　　　　类型：String，默认：process.cwd()
 　　　　 设置输出文件夹路径的相对路径，默认为当前脚本的工作目录的路径。
 　　　options.mode
 　　　　类型：String，默认：0777
 　　　　设置被创建文件夹的权限。
 
 > **gulp.task(name[, deps], fn)**
 
 task方法是gulp用于定义一个具体任务的方法。如果需要执行任务，在终端执行gulp task-name。
 
 语法：
 ```bash
 gulp.task(name[, deps], fn)
 ```
 参数：
 
 name
 　　类型：String， 指任务名，就像上述的eg-1例子的sass。
 deps
 　　类型：Array，指在跑当前任务时，对其它任务的依赖。也就是要执行当前任务，会先执行这些依赖的任务。如: gulp.task('demo', ['demo1', 'demo2'], function(){ });会先同时执行任务'demo1', 'demo2'，最后执行任务'demo'。
 fn
 　　类型：function，指运行任务时，要执行的具体操作的内容。
 
 > **gulp.watch(glob [, opts], tasks) or gulp.watch(glob [, opts, cb])**
 
 watch方法是用于监听文件变化，文件一修改就会执行指定的任务。
 
 语法：
 
 gulp.watch(glob [, opts], tasks) or gulp.watch(glob [, opts, cb])
 
 参数：
 
 glob
 　　类型：String 或 Array，指定源文件的路径，可以是单个路径，也可以是个路径数组。路径匹配和上述gulp.src()方法路径匹配的模式一样。
 opts
 　　类型：Object，有4个属性interval，debounceDelay，mode，cwd。
 　　具体可以参考gulp-api这里就不一一介绍了。
 tasks
 　　类型：Array，监听到文件变化后，要被执行的任务的名字组成的数组。
 cb(event)
 　　类型：Function，监听到变化后，回调的函数。会传递出一个对象类型的event参数。
 　　　event.type
 　　　　类型：String，表示操作的类型：added, changed or deleted
 　　　event.path
 　　　　类型：String，被修改文件的路径。


## 使用例子

```js
var gulp = require('gulp'),
// sass的编译
     sass = require('gulp-ruby-sass'),
// 自动添加css前缀
     autoprefixer = require('gulp-autoprefixer'),
// 压缩css
     minifycss = require('gulp-minify-css'),
// js代码校验
     jshint = require('gulp-jshint'),
// 合并js文件
     concat = require('gulp-concat'),
// 压缩js代码
     uglify = require('gulp-uglify'),
// 压缩图片
     imagemin = require('gulp-imagemin'),
//
     rename = require('gulp-rename'),
// 更改提醒
     notify = require('gulp-notify'),
// 图片缓存，只有图片替换了才压缩
     cache = require('gulp-cache'),
// 自动刷新页面
     livereload = require('gulp-livereload'),
     del = require('del');
     
/**
 *     编译sass  添加前缀  保存到指定目录下 压缩添加.min后缀，输出到指定目录，提示完成
 *     gulp.task这个API用来创建任务，在命令行下可以输入gulp styles来指执行上面的任务
 *     gulp.src要处理的文件的路径，可以是[main.scss,vender.scee],也可以是正则表达式\/**\/*.scss
 *     .pipe()     将处理的文件导向sass插件
 *     gulp.dest() API设置生成文件的路径，一个任务可以有多个生成路径
 */
gulp.task('styles',function () {
     return gulp.src('src/styles/main.scss')
          .pipe(sass({style:'expanded'}))
          .pipe(autoprefixer('last 2 version','safari 5','ie 8'))
          .pipe(rename({suffix:'.min'}))
          .pipe(minifycss())
          .pipe(gulp.dest('dist/assets/css'))
          .pipe(notify({message:'styles task complete'}))
});

/**
 * js代码校验、合并和压缩
 *
 */
gulp.task('scripts',function () {
     return gulp.src('src/scripts/**/*.js')
          .pipe(jshint('.jshintrc'))
          .pipe(jshint.reporter('default'))
          .pipe(concat('main.js'))
          .pipe(gulp.dest('dist/assets/js'))
          .pipe(rename({suffix:'.min'}))
          .pipe(uglify())
          .pipe(gulp.dest('dist/assets/js'))
          .pipe(notify({message:'scripts task complete'}));
});

/**
 * 压缩图片
 * 进一步优化，用缓存保存过的压缩过的图片
 * 将 pipe(imagemin({optimizationLevel:3, progressive: true,interlaced: true}))改成
 *  pipe(cache(imagemin({optimizationLevel:5,progressive:true,interlaced:true})))
 */
gulp.task('images', function () {
     return gulp.src('src/images/**/*')
          .pipe(imagemin({optimizationLevel: 3,progressive: true,interlaced: true}))
          .pipe(gulp.dest('dist/assets/img'))
          .pipe(notify({message: 'images task complete'}));
});


/**
 * 清除文件
 */
gulp.task('clean',function (cb) {
     del(['dist/assets/css','dist/assets/js','dist/assets/img'],cb)
});

/**
 * 设置默认任务（default）
 * sudo gulp就是执行的默认任务
 */
gulp.task('default',['clean'],function(){
     gulp.start('styles','scripts','images')
});

/**
 * 监听文件是否修改以执行相应的任务，
 * 在命令行输入sudo gulp watch
 */
gulp.task('watch',function(){
     gulp.watch('src/styles/**/*.scss',['styles']);
     gulp.watch('src/scripts/**/*.js',['scripts']);
     gulp.watch('src/images/**/*',['images']);
});
/**
 * 自动刷新页面
 * 需要在浏览器上安装LiveReload
 */
gulp.task('watch',function(){
     livereload.listen();
     gulp.watch(['dist/**']).on('change',livereload.changed);
});
```
