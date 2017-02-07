title: nginx 相关
date: 2015-12-28 16:27:31
tags: nginx
---
## 前端代理请求,将请求域名代理掉，解决跨域问题
```nginx
location  /v6/ {
      proxy_set_header X-Forward-For $remote_addr ;
      proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
      proxy_set_header host app.conf.ayibang.com;
      proxy_pass http://app.conf.ayibang.com;
}
```
## 设置expires 和cache-control
```nginx
 location ~ .*\.(git|js|swf|jpg|png|jpeg|bmp|eot|svg|woff|ttf)$ {
       root           ${PRJ_ROOT}/dist/${OUTDIR};
       expires max;
 }
/* max:指定“Expires”的值为31 December2037 23:59:59GMT,"Cache-Control"的值为10年。 */
/* -1：指定“Expires”的值为当前服务器时间-1s，即永远过期。 */
/* off：不修改“Expires”和"Cache-Control"的值 */
```

```nginx
#强制刷新html
location / {
    root           ${PRJ_ROOT}/dist/${OUTDIR}/ ;
    index index_${ENV}.html;
    add_header Cache-Control no-store;
    rewrite ^/index\.html$ /index_${ENV}.html last;
}
```

## nginx设置字符串替换,同时兼容ie
```nginx
 if ( $http_user_agent ~* "MSIE [6-9].[0-9]") {
      set $ua "";
  }
  if ( $http_user_agent !~* "MSIE [6-9].[0-9]") {
      set $ua http://api.com;
  }
 sub_filter  </head>   '</head> <script> window.APPURL= {"USER_URL":"$ua"}</script>' ; #一般可和rg_ng等配置生成工具一起使用作为接口的全局配置
 sub_filter_once on;
 sub_filter_types text/html;

```


##  nginx 设置自定义头
```nginx
 add_header ZLX-URL http://user-gw.com [always]; #1.7.5以上 always 对于任意响应都会有效，否则只对2xx/3xx
```
