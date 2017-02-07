title: ie
date: 2016-11-07 20:45:57
tags:
---



## ie8,ie9 跨域解决方法：
基于常用的jquery采用jQuery-ajaxTransport-XDomainRequest，,如果是post，则数据传递只为text/plain来进行传递，所以php端需要用 php://input获取原始post数据.(此方法无法获取到error中的任何信息包括code，只能通过全部返回200的方法将error放到里面http://stackoverflow.com/questions/10390539/xdomainrequest-get-response-body-on-error),而且`XDoaminRequest`比较弱，跨域`https`，`cookie`等都不支持，所以最好的方法还是`同域代理`。
https://github.com/MoonScript/jQuery-ajaxTransport-XDomainRequest


## 部分ie（ie8，ie9）不能出现console.log，否则当不打开开发者工具的时候，会造成程序终止.


## ie8以及ie8之前的不支持stopPropagation，只能使用cancelBubble,ie9可以支持.

