
# HTTP Request Method

---

### 方法汇总一

方法 | 说明
--- | ---
GET | 从服务端获取指定的资源
POST | 发送特定类型的数据给服务端，进行资源的创建
PUT | 发送数据给服务端，新增资源或替换目标资源
DELETE | 告诉服务端删除指定的资源

--

### 方法汇总二

方法 | 说明
--- | ---
OPTIONS | 获取资源所支持的方法
HEAD | 获取资源的响应头部，与GET获取到的相同
PATCH | 发送数据给服务端，部分修改资源
TRACE | 回显服务器收到的请求，主要用于测试或诊断
CONNECT | HTTP/1.1协议中预留，将连接改为管道方式

---

### 方法的三个属性

 - [安全(Safe)](https://developer.mozilla.org/zh-CN/docs/Glossary/safe)，不改变服务端资源
 - [幂等(Idempotent)](https://developer.mozilla.org/zh-CN/docs/Glossary/%E5%B9%82%E7%AD%89)，多次调用效果相同
 - [可缓存(Cacheable)](https://developer.mozilla.org/en-US/docs/Glossary/Cacheable)，响应可以被客户端缓存

---

## GET

*从服务端获取指定的资源*

属性 | 值
--- | ---
请求是否有主体 | 否
成功的响应是否有主体 | 是
安全 | 是
幂等 | 是
可缓存 | 是
是否支持表单 | 是

--

### Ajax方式

```bash
//请求
GET /api/employees/zhangchunxin
```
<!-- .element: class="fragment visible"--> 


```bash
//响应
HTTP/1.1 200 
Host: 127.0.0.1
ETag: de08b7bc-82d9-40da-b1b9-8ee1b2aff19f
Content-Type: application/json
Content-Length: 67
Date: Tue, 09 Jan 2018 02:56:26 GMT

//响应主体
{"status":"success","data":{"name":"zhangchunxin","id":"00230635"}}
```
<!-- .element: class="fragment visible"--> 

```bash
//另一种请求方式
GET /api/employees/api/employees?name=zhangchunxin
```
<!-- .element: class="fragment visible"--> 

--

### 表单方式

```html
//表单请求
<form method="get" action="/api/employees">
    <input name="name" value="zhangchunxin">
    <input type="submit">
</form>
```
```bash
HTTP/1.1 200 
Host: 127.0.0.1
ETag: de08b7bc-82d9-40da-b1b9-8ee1b2aff19f
Content-Type: application/json
Content-Length: 67
Date: Tue, 09 Jan 2018 02:57:46 GMT

//响应主体
{"status":"success","data":{"name":"zhangchunxin","id":"00230635"}}
```
<!-- .element: class="fragment visible"--> 

---

## POST

*发送特定类型的数据给服务端，进行资源的创建*

属性 | 值 
--- | --- 
请求是否有主体 | 是 
成功的响应是否有主体 | 是 
安全 | 否
幂等 | 否
可缓存 | [看情况](https://stackoverflow.com/questions/626057/is-it-possible-to-cache-post-methods-in-http) 
是否支持表单 | 是 

--

### Ajax方式

```bash
//请求
POST /api/employees
Content-Type: application/json

{
    "name": "luanzhuo",
    "id": "00356107"
}
```
<!-- .element: class="fragment visible"--> 


```bash
//响应
HTTP/1.1 201 
ETag: f55a6fdc-1ac1-4ea2-9b43-f6517c93b3ac
Location: /api/employees/luanzhuo
Content-Type: application/json
Content-Length: 63
Date: Tue, 09 Jan 2018 02:59:45 GMT

//响应主体
{"status":"success","data":{"name":"luanzhuo","id":"00356107"}}
```
<!-- .element: class="fragment visible"--> 

--

### 表单方式

```html
//表单请求
<form method="post" action="/api/employees">
    <input name="name" value="luanzhuo">
    <input name="id" value="00356107">
    <input type="submit">
</form>
```
```bash
HTTP/1.1 201 
ETag: 5c17d201-79c0-464d-bb6f-48fef959aa30
Location: /api/employees/luanzhuo
Content-Type: application/json
Content-Length: 63
Date: Tue, 09 Jan 2018 03:00:20 GMT

//响应主体
{"status":"success","data":{"name":"luanzhuo","id":"00356107"}}
```
<!-- .element: class="fragment visible"--> 

---

## PUT

*发送数据给服务端，新增资源或替换目标资源*

属性 | 值 
--- | --- 
请求是否有主体 | 是 
成功的响应是否有主体 | 都可以
安全 | 否
幂等 | 是
可缓存 | 否 
是否支持表单 | 否 

--

### 创建

```bash
//请求
PUT /api/employees/tiankai
Content-Type: application/json

{
    "name": "tiankai",
    "id": "00226034"
}
```
<!-- .element: class="fragment visible"--> 

```bash
//响应
HTTP/1.1 201 
ETag: 97e7e534-e5b2-4dbf-9aff-885db335581c
Content-Type: application/json
Content-Location: /api/employees/tiankai
Date: Tue, 09 Jan 2018 03:41:41 GMT
```
<!-- .element: class="fragment visible"--> 

--

### 替换

```bash
//请求
PUT /api/employees/tiankai
Content-Type: application/json

{
    "id": "00226034"
}
```
<!-- .element: class="fragment visible"--> 

```bash
//响应
HTTP/1.1 204 
Content-Type: application/json
ETag: b0307586-832f-46fc-bd97-9e1ba30f5f79
Content-Location: /api/employees/tiankai
Date: Tue, 09 Jan 2018 03:42:06 GMT
```
<!-- .element: class="fragment visible"--> 

--

### 修改 OK

```bash
//请求
PUT /api/employees/tiankai
Content-Type: application/json

{
    "id": "00226034"
}
```
<!-- .element: class="fragment visible"--> 

```bash
//响应 修改
HTTP/1.1 200 
ETag: 284b01cd-5e7b-4fd6-9cd8-d0263b8aaaa0
Content-Type: application/json
Content-Length: 62
Date: Tue, 09 Jan 2018 04:02:05 GMT

//响应主体
{"status":"success","data":{"name":"tiankai","id":"00226034"}}
```
<!-- .element: class="fragment visible"--> 

--

### 修改 Not Found

```bash
//请求
PUT /api/employees/tiankai
Content-Type: application/json

{
    "id": "00226034"
}
```
<!-- .element: class="fragment visible"--> 

```bash
//响应 资源不存在
HTTP/1.1 404 
Content-Type: application/json
Content-Length: 67
Date: Tue, 09 Jan 2018 04:01:10 GMT

//响应主体
{"status":"error","message":"employees named tiankai is not exist."}
```
<!-- .element: class="fragment visible"--> 

---

## DELETE

*告诉服务端删除指定的资源*

属性 | 值 
--- | --- 
请求是否有主体 | 否 
成功的响应是否有主体 | 否 
安全 | 否
幂等 | 是
可缓存 | 否 
是否支持表单 | 否 

--

### 删除 OK

```bash
//请求
DELETE /api/employees/tiankai
```
<!-- .element: class="fragment visible"--> 


```bash
//响应 删除
HTTP/1.1 200 
Content-Length: 0
Date: Tue, 09 Jan 2018 04:05:27 GMT
```
<!-- .element: class="fragment visible"--> 

```bash
//另一种请求方式
DELETE /api/employees?name=tiankai
```
<!-- .element: class="fragment visible"--> 

--

### 删除 Not Found

```bash
//请求
DELETE /api/employees/tiankai
```
<!-- .element: class="fragment visible"--> 

```bash
//响应 资源不存在
HTTP/1.1 404 
Content-Length: 0
Date: Tue, 09 Jan 2018 04:09:57 GMT
```
<!-- .element: class="fragment visible"-->

```bash
//另一种请求方式
DELETE /api/employees?name=tiankai
```
<!-- .element: class="fragment visible"--> 

---

## HEAD

*获取资源的响应头部，与GET获取到的相同*

属性 | 值 
--- | --- 
请求是否有主体 | 否 
成功的响应是否有主体 | 否 
安全 | 是
幂等 | 是
可缓存 | 是 
是否支持表单 | 否

--

### 普通方式

```bash
//请求
HEAD /api/employees
```
<!-- .element: class="fragment visible"--> 

```bash
//响应
HTTP/1.1 204 
ETag: 6c919dba-2f90-4625-a13a-7ea3b0950a28
Host: 127.0.0.1
Content-Type: application/json
Date: Tue, 09 Jan 2018 07:12:40 GMT
```
<!-- .element: class="fragment visible"--> 

--

### CORS方式

```bash
//请求
HEAD http://localhost:8080/api/employees
Access-Control-Request-Headers: X_API_employees, Content-Type
```
<!-- .element: class="fragment visible"--> 


```bash
//响应
HTTP/1.1 204 
Access-Control-Allow-Headers: X_API_employees, Content-Type
Access-Control-Allow-Origin: zhangchunxin.inhuawei.com
Access-Control-Max-Age: 86400
Content-Type: application/json
Date: Tue, 09 Jan 2018 07:23:55 GMT
```
<!-- .element: class="fragment visible"--> 

---

## OPTIONS

*获取资源所支持的方法*

属性 | 值 
--- | --- 
请求是否有主体 | 否 
成功的响应是否有主体 | 否 
安全 | 是
幂等 | 是
可缓存 | 否
是否支持表单 | 否 

--

### 普通方式

```bash
//请求
OPTIONS /api/employees
```
<!-- .element: class="fragment visible"--> 


```bash
//响应
HTTP/1.1 204 
Allow: HEAD,DELETE,POST,GET,OPTIONS,PUT
Date: Tue, 09 Jan 2018 06:35:14 GMT
```
<!-- .element: class="fragment visible"--> 

--

### CORS方式

```bash
//请求
OPTIONS /api/employees
Access-Control-Request-Method: POST, GET
```
<!-- .element: class="fragment visible"--> 

```bash
//响应
HTTP/1.1 204 
Access-Control-Allow-Methods: GET
Access-Control-Allow-Origin: zhangchunxin.inhuawei.com
Access-Control-Max-Age: 86400
Date: Tue, 09 Jan 2018 07:27:14 GMT
```
<!-- .element: class="fragment visible"--> 

---

## GET V.S. POST

GET —— 查询资源

POST —— 创建资源

--

### 属性对比一

属性 | GET | POST
--- | --- | ---
可缓存 | 支持 | 不支持
编码类型 | application/x-www-form-urlencoded | 多种
参数长度 | URL限制(2048) | 无限制
参数类型 | ASCII | 无限制

--

### 属性对比二

属性 | GET | POST
--- | --- | ---
安全性 | 数据保存在URL中 | 数据不保存
可见性 | 任何人可见 | 不可见
发送敏感信息 | 不可以 | 可以
刷新/后退(幂等) | 无影响 | 重新提交
书签收藏 | 支持 | 不支持
历史记录 | 包含参数 | 不包含参数

--

### 总结

#### GET
 - 用于查询请求场景
 - 用于安全性要求不高的情况
 - 用于需要缓存的场景
 - 需要保证幂等性

#### POST
 - 用于创建请求场景
 - 用于安全性要求较高的情况
 - 扩展GET查询，支持更复杂的查询条件

---

## POST V.S. PUT

POST —— 创建资源

PUT —— 创建或替换资源

--

### 属性对比

属性 | POST | PUT
--- | --- | ---
请求是否有主体 | 是 | 是
成功的响应是否有主体 | 是 | 都可以
安全 | 否 | 否
幂等 | 否 | 是
可缓存 | [看情况](https://stackoverflow.com/questions/626057/is-it-possible-to-cache-post-methods-in-http) | 否 
是否支持表单 | 是 | 否

--

POST创建请求
```bash
POST /api/employees
Content-Type: application/json

{
    "name": "luanzhuo",
    "id": "00356107"
}
```

PUT修改请求
```bash
PUT /api/employees/tiankai
Content-Type: application/json

{
    "id": "00226034"
}
```

--

### 总结

 - POST和PUT都可以用于创建或修改
 - PUT需要保证幂等性
 - 业界RESTful实践中，POST用作创建，PUT/PATCH用作修改

---

## 全文总结

介绍常见的HTTP方法，希望大家在后续开发中能够保证对应方法的正确性。

--

### 拓扑的HTTP方法规范

方法 | 说明
--- | ---
GET | 查询
POST | 创建
PUT | 修改
DELETE | 删除

---

### 附录

 - [HTTP Protocol Specification - w3](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)
 - [HTTP 请求方法 -MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods)
 - [HTTP Methods: GET vs. POST - 3school](https://www.w3schools.com/tags/ref_httpmethods.asp)
 - [PUT vs. POST in REST - Stack Overflow](https://stackoverflow.com/questions/630453/put-vs-post-in-rest)
 - [源码](http://isource-xa.huawei.com/z00230635/java_practice/tree/master/Spring/aq-spring-demo/src/main/java/aq/springboot/demo/jersey/controller/http/MethodController.java)
