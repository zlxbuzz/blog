title: webpack遇到的坑
date: 2017-03-30 13:03:31
tags: webpack
---

## webpack1构建的时候-webkit-flex消失导致ios8系统样式错乱

```js
/* 原因是构建环境的时候`uglifyjs`可能造成的这个问题，开发模式没有这个问题 */
在配置的时候加上'css-loader?-autoprefixer'就可以了

```

