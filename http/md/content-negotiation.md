
# HTTP Content Negotiation

---

### 请求/响应头

```http
Accept:application/json, text/javascript, */*; q=0.01
Accept-Encoding:gzip, deflate, br
Accept-Language:zh-CN,zh;q=0.9
```
<!-- .element: class="fragment visible"--> 

```http
Cache-Control:no-cache, no-store, max-age=0, must-revalidate
Connection:keep-alive
Content-Length:123
Content-Type:application/json;charset=UTF-8
```
<!-- .element: class="fragment visible"--> 

--

### 内容协商示意

![](https://img.zhangchunxin.com/reveal/http/content-negotiation/e2a2c3e3.png)

[Back](#/1)

---

## 主动协商机制

![](https://img.zhangchunxin.com/reveal/http/content-negotiation/HTTPNegoServer.png)

客户端携带HTTP请求头部，主动与服务端协商

---

## 主动协商的头部

请求头部 | 说明 | 举例
--- | --- | ---
Accept | 客户端期望接收的资源的MIME类型 | application/json
Accept-Charset | 告知服务器客户端期望的字符编码 | utf-8,*;q=0.7
Accept-Language | 告诉客户端期望的自然语言 | zh,en;q=0.7
Accept-Encoding | 说明客户端所期望的压缩算法 | br,gzip;q=0.8
<!-- .element: style="font-size: 28px;"-->
</br>

响应头部 | 说明 | 举例
--- | --- | ---
Vary | 告诉客户端可以使用哪些头部信息来协商资源 | Accept
<!-- .element: style="font-size: 28px;"--> 

---

### Accept

客户端希望接收的资源的MIME类型

*[常见浏览器的Accept头部默认取值](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Content_negotiation/List_of_default_Accept_values)*

--

#### Accept: application/xml

```http
GET /api/negotiation/employee/00230635
Accept: application/xml
```
<!-- .element: class="fragment visible"--> 

```http
HTTP/1.1 200 
Content-Type: application/xml
Date: Wed, 17 Jan 2018 09:02:23 GMT

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<response>
    <status>success</status>
    <data>
        <id>00230635</id>
        <name>zhangchunxin</name>
    </data>
</response>
```
<!-- .element: class="fragment visible"--> 

--

#### Accept: application/json

```http
GET /api/negotiation/employee/00230635
Accept: application/json
```
<!-- .element: class="fragment visible"--> 

```http
HTTP/1.1 200 
Content-Type: application/json
Date: Wed, 17 Jan 2018 09:04:35 GMT

{
    "status":"success",
    "data":
        {
            "id":"00230635",
            "name":"zhangchunxin"
        }
}
```
<!-- .element: class="fragment visible"--> 

---

### Accept-Language

告诉客户端期望的自然语言

--

#### Accept-Language: en_US

```http
GET /api/negotiation/employee/00230635
Accept: application/json
Accept-Language: en_US
```
<!-- .element: class="fragment visible"--> 

```http
HTTP/1.1 200 
Content-Language: en_US
Content-Type: application/json
Date: Wed, 17 Jan 2018 09:13:22 GMT

{"status":"success","data":{"id":"00230635","name":"zhangchunxin"}}
```
<!-- .element: class="fragment visible"--> 

--

#### Accept-Language: zh_CN

```http
GET /api/negotiation/employee/00230635
Accept: application/json
Accept-Language: zh_CN
```
<!-- .element: class="fragment visible"--> 

```http
HTTP/1.1 200 
Content-Language: zh_CN
Content-Type: application/json
Date: Wed, 17 Jan 2018 09:13:52 GMT

{"status":"success","data":{"id":"00230635","name":"张春鑫"}}
```
<!-- .element: class="fragment visible"--> 

---

### Accept-Charset

告知服务器客户端支持的字符编码

--

#### Accept-Charset: utf-8

```http
GET /api/negotiation/employee/00230635
Accept: application/json
Accept-Charset: utf-8
Accept-Language: en_US
```
<!-- .element: class="fragment visible"--> 

```http
HTTP/1.1 200 
Content-Language: en_US
Content-Type: application/json;charset=utf-8
Date: Wed, 17 Jan 2018 09:10:29 GMT

{"status":"success","data":{"id":"00230635","name":"zhangchunxin"}}
```
<!-- .element: class="fragment visible"--> 

--

#### Accept-Charset: ascii

```http
GET /api/negotiation/employee/00230635
Accept: application/json
Accept-Charset: ascii
```
<!-- .element: class="fragment visible"--> 

```http
HTTP/1.1 200 
Content-Language: en_US
Content-Type: application/json;charset=ascii
Date: Wed, 17 Jan 2018 09:11:29 GMT

{"status":"success","data":{"id":"00230635","name":"zhangchunxin"}}
```
<!-- .element: class="fragment visible"--> 

--

#### Language与Charset不匹配

```http
GET http://localhost:8080/api/negotiation/employee/00230635
Accept: application/json
Accept-Language: zh_CN
Accept-Charset: ascii
```
<!-- .element: class="fragment visible"--> 

```http
HTTP/1.1 200 
Content-Language: zh_CN
Content-Type: application/json;charset=ascii
Date: Wed, 17 Jan 2018 09:33:35 GMT

{"status":"success","data":{"id":"00230635","name":"���������"}}
```
<!-- .element: class="fragment visible"--> 

```http
HTTP/1.1 400 
Content-Type: application/json;charset=ascii
Date: Wed, 17 Jan 2018 09:29:23 GMT
Connection: close

{"status":"error","message":"Invalid the charset ascii of language zh_CN"}
```
<!-- .element: class="fragment visible"--> 

---

### Accept-Encoding

说明客户端所期望的压缩算法

见[HTTP Compression](/reveal/http/compression.html)

---

### Vary

告诉客户端可以使用哪些头部信息来协商资源

--

#### 样例

```http
GET /api/negotiation/employee/00230635
```
<!-- .element: class="fragment visible"--> 

```http
HTTP/1.1 200 
Vary: Accept,Accept-Language,Accept-Encoding
Content-Language: en_US
Content-Type: application/json;charset=utf-8
Date: Wed, 17 Jan 2018 09:20:11 GMT

{"status":"success","data":{"id":"00230635","name":"zhangchunxin"}}
```
<!-- .element: class="fragment visible"--> 

---

### 附录

 - [内容协商 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Content_negotiation)
 - [CONTENT NEGOTIATION: WHY IT IS USEFUL, AND HOW TO MAKE IT WORK - W3 Blog](https://www.w3.org/blog/2006/02/content-negotiation)
 - [Understanding HTTP content negotiation - Thierry Templier - Restlet](http://restlet.com/company/blog/2015/12/10/understanding-http-content-negotiation)
 - [REST – Content Negotiation - REST API Tutorial](https://restfulapi.net/content-negotiation)
 - [源码 - iSource](http://isource-xa.huawei.com/z00230635/java_practice/tree/master/Spring/aq-spring-demo/src/main/java/aq/springboot/demo/jersey/controller/http/NegotiationController.java)