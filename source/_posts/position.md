title: angular-ui-bootstrap $position源码分析
date: 2016-02-25 19:56:40
tags: angular
---
`$position` 是`angular-bootstrap`实现的一个获取定位元素位置的服务。代码的大致结构为:
```js
.factory('$position', ['$document', '$window', function ($document, $window) {
    function getStyle(el, cssprop) {}
    function isStaticPositioned(element) {}
    //返回3个方法
    return {
        position:function(){}//计算具体元素的定位地址，返回一个带有width、height、top、left的对象
        offset:function(){} //返回元素相对于文档的偏移量
        positionElements:function(){} //返回某元素相对于其依赖容器元素的定位位置
    }
})

```

