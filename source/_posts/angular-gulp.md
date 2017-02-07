title: 常见的gulp任务
date: 2016-02-15 14:45:38
tags: gulp
---
##  gulp-ng-html2js
```js
//将模版文件存到angular的$templateCache中,相当于无需加载额外的模版
var templateFiles = "src/**/*.{tpl,md}";
var markdown      = require('gulp-markdown');
var ngHtml2js     = require('gulp-ng-html2js');
gulp.src(templateFiles)
.pipe(gulpif('*.md', markdown()))
.pipe(rename({
        extname: ".tpl"
    }))
.pipe(ngHtml2js({
        moduleName: "components",//angular对应的模块名
        prefix: 'components/',//$templateCache的名称的前缀("$templateCache.put(prefix)")
        declareModule : false//不需要独立的模块
    }))
.pipe(concat("template.js"))
.pipe(gulp.dest('./'));
}))
```


## gulp-rev-all
    有个坑，需要自定义replacer函数来过滤，否则内容中和文件同名的也会加hash。
    https://github.com/smysnk/gulp-rev-all/issues/106
```js
gulp.task('rev_all',function(){
    return gulp.src(releasePath+'/**')
        .pipe(revAll.revision({
            dontRenameFile: [/^\/favicon.ico$/g, '.html'],
            prefix: 'http://res.mararun.com/online/louis-web',
            replacer:replacer
        }))
        .pipe(gulp.dest(onlinePath));
});
function replacer(fragment, replaceRegExp, newReference, referencedFile) {
    if(referencedFile.revFilenameExtOriginal === '.js' && !replaceRegExp.toString().match(/\.js/)){
        return;
    }
   fragment.contents = fragment.contents.replace(replaceRegExp, '$1' + newReference + '$3$4');
}

```


## gulp-plumber

```js
//错误处理一般用plumber来提醒，不过最好搭配gulp-notify。否则可能会出现中断的问题，加上这个就没有问题了。
.pipe(plumber({errorHandler: notify.onError('Error: <%= error.message %>')}))

```
