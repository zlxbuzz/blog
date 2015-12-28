title: nginx 相关
date: 2015-12-28 16:27:31
tags: nginx
---
前端代理请求,将请求域名代理掉，解决跨域问题
```nginx
location  /v6/ {
      proxy_set_header X-Forward-For $remote_addr ;
      proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
      proxy_set_header host app.conf.ayibang.com;
      proxy_pass http://app.conf.ayibang.com;
}
```
