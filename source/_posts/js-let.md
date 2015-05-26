title: ES6中的let和const
date: 2015-04-27 15:06:24
categories: js
tags: js
---
在`ES6`中新增了`let`,`const`,(`use strict`下)，他们拥有块级作用域，可以取代`var`.
```js
if (true) {
  let a = 1;
  var b = 2;
}
console.log(a); // ReferenceError: a is not defined
console.log(b); //2
```
`for`引用
```js
var funcs = {};
for(let i = 0; i < 3; i++) {
  funcs[i] = function() {
    console.log(i);
  }
}
funcs[0](); // 0 
```
Temporal Dead Zone
```js
let x = 1;
(function() {
  console.log(x); // ReferenceError: x is not defined
  let x = 2;//这行如果没有,则x会获取父级的 1  如果作用域内有let的TDZ会使x未赋值,var则不会
})();
```
