title: webpack遇到的坑
date: 2017-03-30 13:03:31
tags: webpack
---

## webpack1

构建的时候-webkit-flex消失导致ios8系统样式错乱
```js
/* 原因是构建环境的时候`uglifyjs`可能造成的这个问题，开发模式没有这个问题 */
在配置的时候加上'css-loader?-autoprefixer'就可以了
```

`new webpack.optimize.CommonsChunkPlugin` 改变publicpath但是chunkhash不变


```js
当改变publicpath的时候chunkhash值不会变，但是内容会变，会导致cdn资源被覆盖,一般就会采用hash，
此问题在webpack2中已经解决

```

## webpack2 构建遇到不同开发目录chunkhash不一致

```js

目前原因未知，当有vue引入的时候，改变项目的目录会导致chunkhash变换
```


## webpack-dev-server2 invalid host header

```js
//直接使用localhost和127.0.0.1都可以正常访问，但是使用ip就会显示invalid host header,原因是webpack会检测hostname是否在配置内，不再的话就会报错，直接禁止检测即可
devServer: {
      disableHostCheck: true
}
```

