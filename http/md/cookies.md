
# HTTP Cookies

---

![](https://img.zhangchunxin.com/reveal/http/cookies/db434624.png)

保存在浏览器中的一小块数据

---

## Cookie长什么样

--

### Chrome Console

```javascript
document.cookie
```

```bash
csrftoken=jgKU1wGm0E0J5T4ppMbRfi0JjbfnnmET;
dwf_sg_task_completion=False;
_ga=GA1.2.1415569057.1506301776;
optimizelyEndUserId=oeu1520818572540r0.9742016353524761;
optimizelySegments=%7B%22245617832%22%3A%22none%22%2C%22245677587%22%3A%22gc%22%2C%22245875585%22%3A%22direct%22%2C%22246048108%22%3A%22false%22%2C%228405160556%22%3A%22true%22%7D;
optimizelyBuckets=%7B%7D;
_gid=GA1.2.1353051980.1522219538;
_gat=1
```

--

### Chrome Application

![](https://img.zhangchunxin.com/reveal/http/cookies/bd09948c.png)

--

### HTTP Header

![](https://img.zhangchunxin.com/reveal/http/cookies/f17f8fa2.png)

---

## Cookie的属性

属性 | 含义 | 举例
--- | --- | ---
Name | Cookie的键值 | csrftoken
Value | Cookie的值 | jgKU1wGm0E0J5T4ppMbRfixxxfnnmET
Domain | Cookie生效的域名 | mozilla.org
Path | Cookie生效的路径 | /
Expires | Cookie的过期时间(HTTP/1.0) | Thu, 25 Feb 2019 04:18:00 GMT<br>Session
Max-Age | Cookie的最长生存时间 | 600<br>Session
HttpOnly | Cookie是否仅通过HTTP访问 | N/A
Secure | Cookie是否仅允许HTTPS传输 | N/A
SameSite | Cookie是否允许跨站传输(试验阶段) | N/A
<!-- .element: style="font-size: 26px;"-->

--

### 一个完整的Cookie

`csrftoken=jgKU1wGm0E0J5T4ppMbRfixxxfnnmET; expires=Thu, 25 Feb 2019 04:18:00 GMT; domain=mozilla.org; path=/; secure; HttpOnly`

---

## 创建Cookie

--

### 客户端创建

`document.cookie = 'cookie=Milk Cookie'`

![](https://img.zhangchunxin.com/reveal/http/cookies/adf744b0.png)

> 注意
<!-- .element: style="font-size: 28px;"-->

> - 客户端可以设置Expires、Domain、Path、Secure（只在HTTPS协议的网页可以设置），无法设置HttpOnly
<!-- .element: style="font-size: 26px;"-->
> - Expires默认为Thu Jan 01 1970 07:59:59 GMT，Domain默认为当前页面的域名，Path默认为当前页面的路径
<!-- .element: style="font-size: 26px;"-->
> - 一行JavaScript语句只能设置一个Cookie
<!-- .element: style="font-size: 26px;"-->

--

### 服务端创建

响应头部 | 说明 | 举例
--- | --- | ---
Set-Cookie | 返回给客户端设置Cookie | Set-Cookie: cookie=Chocolate Cookie;Path=/
<!-- .element: style="font-size: 26px;"-->

![](https://img.zhangchunxin.com/reveal/http/cookies/25de08da.png)

> 注意：
<!-- .element: style="font-size: 26px;"-->
> 一个Set-Cookie头只能设置一个Cookie
<!-- .element: style="font-size: 26px;"-->

---

## 修改Cookie

对已有Cookie重新赋值即可

`document.cookie = 'cookie=Honey Cookie;Domain=localhost;Path=/'`

> 前提：需要保证Name、Domain和Path相同，否则可能会新建Cookie
<!-- .element: style="font-size: 26px;"-->

---

## 删除Cookie

对已有Cookie设置一个过去的时间即可

`document.cookie='cookie=Honey Cookie;Domain=localhost;Path=/;Expires=Thu Jan 01 1970 08:00:00 GMT'`
或
`document.cookie='cookie=Honey Cookie;Domain=localhost;Path=/;Max-Age=-1'`

---

Cookie在物理拓扑里能做什么用？
<!-- .element: style="font-size: 50px;"-->

---

### 附录

 - [聊一聊 cookie by ruoyiqing - segmentfault](https://segmentfault.com/a/1190000004556040)
 - [HTTP cookies - MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)

--

### 扩展阅读

 - [Cookies and security by Nicholas C. Zakas](https://www.nczonline.net/blog/2009/05/12/cookies-and-security/)
 - [HTTP cookies explained by Nicholas C. Zakas](https://www.nczonline.net/blog/2009/05/05/http-cookies-explained/)
 - [Cookies and Sessions by John Ousterhout](https://web.stanford.edu/~ouster/cgi-bin/cs142-fall10/lecture.php?topic=cookie)