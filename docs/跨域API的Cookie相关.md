# 跨域API的Cookie相关
跨域API访问本身还是比较简单的，基本上就是两个条件：
1. 响应OPTIONS请求。
2. 在所有请求中加上CORS的允许头：`Access-Control-Allow-Origin`, `Access-Control-Request-Method`, `Access-Control-Request-Headers`。
* 其中`Access-Control-Allow-Origin`是用来指定允许的`origin`。如果是`*`，代表允许所有。
* `Access-Control-Request-Method`是用来指定允许的方法，比如`GET`, `PUT`, `POST`等等。
* `Access-Control-Request-Headers`是用来指定允许的Header的属性。

做到了这一点，Ajax请求就可以在浏览器中跨域了。但是如果有`Cookie`，在跨域请求中仍然不会发送到服务器上。
这个时候在响应中需要一个新的Header属性，`Access-Control-Allow-Credentials`，需要设为`true`。相对应的，客户端需要加上如下的代码
```javascript
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;
```
然后`Access-Control-Allow-Origin`必须是特定的`Origin`，不能是`*`。
在服务器端设置`Cookie`的时候，需要设置一个`Domain`的属性，而且，前端代码的`Origin`和后端必须要在一个域名下，例如`a.a.com`和`b.a.com`的时候，那`Domain`就设为`a.·com`。
