title: web 安全相关
date: 2016-03-27 10:55:08
tags: http
---

## 防止clickjacking(点击劫持)

```js
//阻止任何页面对当前页面在iframe中进行加载
res.set({`X-FRAME-OPTIONS` : `DENY`});

//通过js 控制
<style>
  body {
    display : none
  }
</style>
<script>
  (function(){
    if(self == top){
        var theBody = document.getElementsByTagName('body')[0];
        theBody.style.display = "block";
    }else{
        top.location = self.location;
    }
  })()
</script>
```
