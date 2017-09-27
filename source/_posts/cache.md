title: 移动端回退产生缓存不执行js
date: 2017-06-27 10:36:46
tags: m
---

参考来源：https://juejin.im/entry/58882350b123db16a344c74a

```js
　//PC浏览器，设置禁用页面缓存header即可实现后退刷新
  res.header('Cache-Control', 'private, no-cache, no-store, must-revalidate');
  res.header('Expires', '-1');
  res.header('Pragma', 'no-cache');
```

```js
 //支持bfcache/page cache的移动端浏览器，JS监听pageshow/pagehide
 window.onpageshow = function(event) {
     if (event.persisted) {
         window.location.reload()
     }
 };
```


```js
/*在HTML中写入服务端页面生成版本号，与本地存储中的版本号对比判断是否发生了后退并使用缓存中的页面 */
<!-- 安卓webview 后退强制刷新解决方案 START -->
<jsp:useBean id="now" class="java.util.Date" />
<input type="hidden" id="SERVER_TIME" value="${now.getTime()}"/>
<script>
//每次webview重新打开H5首页，就把server time记录本地存储
var SERVER_TIME = document.getElementById("SERVER_TIME");
var REMOTE_VER = SERVER_TIME && SERVER_TIME.value;
if(REMOTE_VER){
    var LOCAL_VER = sessionStorage && sessionStorage.PAGEVERSION;
    if(LOCAL_VER && parseInt(LOCAL_VER) >= parseInt(REMOTE_VER)){
        //说明html是从本地缓存中读取的
        location.reload(true);
    }else{
        //说明html是从server端重新生成的，更新LOCAL_VER
        sessionStorage.PAGEVERSION = REMOTE_VER;
    }
}
</script>
<!-- 安卓webview 后退强制刷新解决方案 END -->

```
