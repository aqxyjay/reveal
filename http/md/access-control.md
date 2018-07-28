
# HTTP Access Control

--

当一个资源从与该资源所在服务器不同的域或端口请求另一个资源时，就会发起一个跨域HTTP请求

出于安全性考虑，需要对这种请求进行HTTP的接入控制

这种特性也叫 ——

--

# Cross-Origin Resource Sharing
<!-- .element: style="font-size: 96px;"-->
# (CORS)
<!-- .element: style="font-size: 88px;"-->

---

## CORS相关的HTTP头

--

### 请求头

请求头 | 含义 | 取值举例
--- | --- | ---
Origin | 表示预检请求或实际请求的源站 | *
Access-Control-Request-Method | 告诉服务器将使用的HTTP方法 | GET, POST
Access-Control-Request-Headers | 告诉服务器将使用的HTTP头 | Cache-Control, X-MyCustomHeader
<!-- .element: style="font-size: 24px;"-->

--

### 响应头

响应头 | 含义 | 取值举例
--- | --- | ---
Access-Control-Allow-Origin | 指定允许访问该资源的外域URI | http://zhangchunxin.inhuawei.com
Access-Control-Allow-Methods | 指定客户端允许使用的HTTP方法 | GET, POST
Access-Control-Allow-Headers | 指定客户端允许使用的HTTP头 | Cache-Control, X-MyCustomHeader
Access-Control-Expose-Headers | 允许浏览器访问的头部白名单 | X-My-Custom-Header, X-Another-Custom-Header
Access-Control-Max-Age | 预检请求的结果能够被缓存多久 | 86400
Access-Control-Allow-Credentials | 当请求的Credentials设置为true时，决定是否允许浏览器读取response的内容 | true
<!-- .element: style="font-size: 22px;"-->

---

## Cross-origin请求

![](https://img.zhangchunxin.com/reveal/http/access-control/b6b90832.png)

---

## 简单请求
#### Simple Request

即使是跨域访问，但有一些请求是不会触发CORS的

这样的请求就叫简单请求

--

### 简单请求的条件

满足*全部*条件

条件 | 匹配值
--- | ---
HTTP Method | GET/HEAD/POST
HTTP Header | Accept<br>Accept-Language<br>Content-Language<br>Content-Type(额外限制，见下一行)
Content-Type | text/plain<br>multipart/form-data<br>application/x-www-form-urlencoded
<!-- .element: style="font-size: 32px;"-->

--

### 举例

![](https://img.zhangchunxin.com/reveal/http/access-control/b6a86675.png)

--

#### 请求

```http
GET /resources/public-data/ HTTP/1.1
Host: bar.other
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Origin: http://foo.example
```

--

#### 响应

```http
HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 00:23:53 GMT
Server: Apache/2.0.61 
Access-Control-Allow-Origin: *
Transfer-Encoding: chunked
Content-Type: application/xml

[XML Data] //响应内容
```

---

## 预检请求
#### Preflight Request

与前述简单请求不同，客户端在发起实际请求前，需要先用OPTIONS方法发起一个预检请求到服务器，来获知服务器是否允许该实际请求

--

### 预检请求的条件

满足*任一*条件

条件 | 匹配值
--- | ---
HTTP Method | PUT/DELETE/PATCH/OPTIONS/CONNECT/TRACE
HTTP Header | 非Accept<br>Accept-Language<br>Content-Language<br>Content-Type(额外限制，见下一行)
Content-Type | 非text/plain<br>multipart/form-data<br>application/x-www-form-urlencoded
<!-- .element: style="font-size: 32px;"-->

--

### 举例

![](https://img.zhangchunxin.com/reveal/http/access-control/86a59c49.png)

--

#### 预检请求

```http
OPTIONS /resources/post-here/ HTTP/1.1
Host: bar.other
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Origin: http://foo.example
Access-Control-Request-Method: POST
Access-Control-Request-Headers: X-PINGOTHER, Content-Type
```

--

#### 预检响应

```http
HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 01:15:39 GMT
Server: Apache/2.0.61 (Unix)
Access-Control-Allow-Origin: http://foo.example
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: X-PINGOTHER, Content-Type
Access-Control-Max-Age: 86400
Vary: Accept-Encoding, Origin
Content-Encoding: gzip
Content-Length: 0
Content-Type: text/plain
```

--

#### 实际请求

```http
POST /resources/post-here/ HTTP/1.1
Host: bar.other
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Connection: keep-alive
X-PINGOTHER: pingpong
Content-Type: text/xml; charset=UTF-8
Referer: http://foo.example/examples/preflightInvocation.html
Content-Length: 55
Origin: http://foo.example
Pragma: no-cache
Cache-Control: no-cache

<?xml version="1.0"?><person><name>Arun</name></person>
```

--

#### 实际响应

```http
HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 01:15:40 GMT
Server: Apache/2.0.61 (Unix)
Access-Control-Allow-Origin: http://foo.example
Vary: Accept-Encoding, Origin
Content-Encoding: gzip
Content-Length: 235
Content-Type: text/plain

[Some GZIP'd payload]
```

---

## 带身份凭证的请求

基于HTTP Cookies和HTTP认证信息发送身份凭证到服务器，然后由服务器响应中的Access-Control-Allow-Credentials头决定客户端是否可以读取响应内容

值 | 含义
--- | ---
true | 可以读取响应
false | 不可以读取响应

--

### 举例

![](https://img.zhangchunxin.com/reveal/http/access-control/5f4d27f9.png)

--

#### 请求

```http
GET /resources/access-control-with-credentials/ HTTP/1.1
Host: bar.other
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Referer: http://foo.example/examples/credential.html
Origin: http://foo.example
Cookie: pageAccess=2
```

--

#### 响应

```http
HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 01:34:52 GMT
Server: Apache/2.0.61 (Unix)
X-Powered-By: PHP/5.2.6
Access-Control-Allow-Origin: http://foo.example
Access-Control-Allow-Credentials: true
Cache-Control: no-cache
Pragma: no-cache
Set-Cookie: pageAccess=3; expires=Wed, 31-Dec-2008 01:34:53 GMT
Vary: Accept-Encoding, Origin
Content-Encoding: gzip
Content-Length: 106
Content-Type: text/plain

[text/plain payload]
```

--

#### 带身份凭证的请求与通配符

对于附带身份凭证的请求，服务器不得设置 Access-Control-Allow-Origin 的值为“*”

---

## 总结

 - **CORS是浏览器针对脚本请求的安全性约束**
 - **在HTTPS中无法发起HTTP跨站请求(Chrome/Firefox)**

---

### 附录

 - [Cross Origin Resource Sharing (CORS) with Jersey - Philipp Wagner - bytefish.de](https://bytefish.de/blog/cors_with_jersey/)
 - [HTTP访问控制（CORS） - MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)
 - [跨域资源共享 CORS 详解 - 阮一峰](http://www.ruanyifeng.com/blog/2016/04/cors.html)