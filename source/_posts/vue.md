title: vue组件开发遇到的问题
date: 2017-05-04 13:59:58
tags: vue
---

## 运行依赖

采用`yarn`安装所需要的运行依赖，比如`vue`,为了保证版本一致，将这些依赖放到`devDependencies`,`peerDevDependencies`。当应用该组件的时候，如果和原来项目中的依赖版本不一致，则会爆出提醒.


## 不直接操作子组件的prop值，尽量采用computed或者data
```js
之前遇到props无法watch的情况，原因是v-if为false的时候将属性的默认值覆盖了，需要注意

```
