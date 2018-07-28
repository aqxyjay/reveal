
# HTTP Authentication

---

## HTTP认证框架

![](https://img.zhangchunxin.com/reveal/http/authentication/d883b116.png)

--

### 认证的HTTP头部

头部 | 类型 | 说明
--- | --- | ---
WWW-Authenticate | 响应头 | 用于告诉客户端使用哪种认证方式
Authorization | 请求头 | 用于服务器认证客户端
Proxy-Authenticate | 响应头 | 通过代理认证，用于告诉客户端使用哪种认证方式
Proxy-Authorization | 请求头 | 通过代理认证，用于代理服务器认证客户端
<!-- .element: style="font-size: 30px;"--> 

--

### 认证的几种方案

方案 | 说明 
--- | --- 
HTTP BASIC Authentication | 使用用户名和密码作为凭证，使用Base64进行编码
HTTP Digest Authentication | 使用用户名和密码作为凭证，对密码先哈希，再发送 
Form-based Authentication | 使用用户名和密码作为凭证，通过表单方式，提交到服务端进行认证
Token-based Authentication | 源于OAuth认证方式，将用户名和密码发送给服务器，服务端返回Token并定时更新
X.509 Certificate Authentication | 通过证书方式进行认证，客户端本地保存私钥，服务端配置公钥
<!-- .element: style="font-size: 30px;"--> 

---

## HTTP BASIC Authentication

--

### 第一步

客户端请求服务端页面

```http
GET /redis/index.html HTTP/1.1
```

--

### 第二步

服务端响应客户端401

```http
HTTP/1.1 401 
Content-Length: 188
Content-Type: text/html
Date: Sat, 27 Jan 2018 10:13:38 GMT
Server: nginx
WWW-Authenticate: Basic realm="Restricted Access!"

<html>
    <head>
        <title>401 Authorization Required</title>
    </head>
    <body bgcolor="white">
        <center>
            <h1>401 Authorization Required</h1>
        </center>
        <hr>
        <center>nginx</center>
    </body>
</html>
```

--

### 第三步

客户端弹出认证对话框

![](https://img.zhangchunxin.com/reveal/http/authentication/d07af2e2.png)

--

### 第四步

输入用户名和密码进行认证

```http
GET /redis/index.html HTTP/1.1
Authorization: Basic ejAwMj***************3NzMw==
```

--

### 第五步

服务端认证成功

```http
HTTP/1.1 200 
Content-Length: 14207
Content-Type: text/html; charset=utf-8
Date: Sat, 27 Jan 2018 10:19:37 GMT
ETag: W/"377f-Y6jHzMulDsHFEuEAJvPAaQ"
Server: nginx

<!DOCTYPE html>
<html>
...略，index.html页面内容
</html>
```

---

## Token-based Authentication

![](https://img.zhangchunxin.com/reveal/http/authentication/b164e483.png)

--

### 第一步

发送用户名和密码到服务端

```http
POST /api/login
Content-Type: application/json
# CHINA域用户名和密码

{
    "name": "pmail_imapmail",
    "password": "iMAP_robot02"
}
```

--

### 第二步

服务端对用户名和密码进行认证，并返回Token

```http
HTTP/1.1 200 
Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJwbWFpbF9pbWFwbWFpbCIsInJvbGVzIjoidXNlciIsImlhdCI6MTUxNzE5NzkwMX0.iqiZyg7IcqEr_qn1VRVYSg__f4-JbCA2javM_hlonKg
Content-Type: text/plain;charset=UTF-8
Content-Length: 19
Date: Mon, 29 Jan 2018 03:51:42 GMT

Login Successfully!
```

--

### 第三步

客户端使用Token继续访问服务端

```http
GET /api/secure/token
Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJwbWFpbF9pbWFwbWFpbCIsInJvbGVzIjoidXNlciIsImlhdCI6MTUxNzE5NzkwMX0.iqiZyg7IcqEr_qn1VRVYSg__f4-JbCA2javM_hlonKg
```

--

### 第四步

服务端认证Token有效性，返回请求结果

```http
HTTP/1.1 200 
Content-Type: text/plain;charset=UTF-8
Content-Length: 20
Date: Mon, 29 Jan 2018 03:53:15 GMT

Your token is valid!
```

---

## 总结

介绍了2种认证方式：

 - HTTP BASIC Authentication，用于演示认证框架，由于安全性较差，已经不怎么使用了
 - Token-based Authentication，属于常用认证方式，可以借鉴学习
 
注：所有认证，必须在服务端进行

---

### 附录

 - [HTTP 身份验证 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Authentication)
 - [身份验证的几种方案 - ntop - 简书](https://www.jianshu.com/p/eaf9197abb6b)
 - [HTTP 基本认证 - Wikiwand](https://www.wikiwand.com/zh/HTTP%E5%9F%BA%E6%9C%AC%E8%AE%A4%E8%AF%81)
 - [HTTP 摘要认证 - Wikiwand](https://www.wikiwand.com/zh/HTTP%E6%91%98%E8%A6%81%E8%AE%A4%E8%AF%81)
 - [HTTP+HTML form-based authentication - Wikiwand](https://www.wikiwand.com/en/HTTP%2BHTML_form-based_authentication)
 - [理解OAuth 2.0 - 阮一峰](http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html)
 - [Authorization - Postman](https://www.getpostman.com/docs/postman/sending_api_requests/authorization)