title: 在用phalcon进行restful时遇到的一个小坑
date: 2015-04-14 17:06:14
categories: [php,restful]
tags: [restful]
---
在用`angular`和`phalcon`做前后端交互的时候，由于前端主要采用了`ngResource`，在进行访问请求的时候，由于后台目录设置的结构为 `api/users` ,
前端设置服务的时候
```js
angular.module('appService', ['ngResource'])
.factory('userService',function($resource){
	return $resource('/api/users/:uid',{uid:'@uid'},{update:{method:'PUT'}});
})

```
如果想要获取所有的用户不传id，由于目录的存在,前端会默认访问 `api/users` 而不是 `api/users/`，从而倒是`301`转移。所以一般会在目录下设置虚拟的参数用来传递，或者约定必须传值，通过不同值进行后台选择处理。

```js
angular.module('appService', ['ngResource'])
.factory('userService',function($resource){
	return $resource('/api/users/users/:uid',{uid:'@uid'},{update:{method:'PUT'}});
})

```
