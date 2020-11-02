问题描述：

先用node开启了一个vue项目的服务（项目一），提示两个地址都可以访问：

```powershell
 App running at:
 -  Local:   http://localhost:3000/
 -  Network: http://192.168.4.154:3000/
```

在浏览中访问这两个地址，都可以访问项目一，`127.0.0.1:3000`也是一样的。

同时，用docsify又开启了另一个服务（项目二），提示可以访问如下地址：

```powershell
Serving F:\niuxiaolin\mdnote\docs now.
Listening at http://localhost:3000
```

这时候浏览器 `http://192.168.4.154:3000/`访问的是项目一，`http://127.0.0.1:3000`也是项目一。而`http://localhost:3000`，访问的是项目二。

如果反过来，先用docsify开启项目二，那么三种方式都是可以访问项目二。此时再用node开启项目一服务，会变成3001端口。



解决： 朋友推荐了解一下HTTP。先看看《图解HTTP》入个门。看完回来补充。