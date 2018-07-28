
# HTTP Response Code

---

### 1xx 信息响应

表示请求已被接受，需要继续处理

--

状态码 | 原因短语 | 详细说明
--- | --- | ---
[100](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/100) | Continue | 表示目前为止一切正常，客户端应该继续请求，如果已请求则忽略
[101](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/101) | Switching Protocols | 表示服务器应客户端升级协议的请求(Upgrade请求头)正在进行协议切换
102 | Processing | 表示服务器已收到并正在处理该请求，但没有响应可用
<!-- .element: style="font-size: 24px;"--> 

---

### 2xx 成功响应

表示请求已成功被服务器接收、理解、并接受

--

状态码 | 原因短语 | 详细说明
--- | --- | ---
[200](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/200) | OK | 表明请求已经成功
[201](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/201) | Created | 该请求已成功，并创建了一个新的资源
[202](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/202) | Accepted | 请求已经接收到，但还未响应，没有结果
[203](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/203) | Non-Authoritative Information | 表示请求成功，但经过了proxy修改
[204](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/204) | No Content | 成功处理了请求，没有返回任何内容
[205](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/205) | Reset Content | 成功处理了请求，没有返回任何内容，同时要求客户端重置文档视图
[206](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/206) | Partial Content | 已经成功处理了部分GET请求
<!-- .element: style="font-size: 24px;"--> 

---

### 3xx 重定向

表示需要客户端采取进一步的操作才能完成请求

--

状态码 | 原因短语 | 详细说明
--- | --- | ---
[300](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/300) | Multiple Choices | 表示重定向的响应状态码，表示该请求拥有多种可能的响应
[301](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/301) | Moved Permanently | 请求的资源已经永久移动到了Location头部指定的URL上
[302](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/302) | Found | 请求的资源被暂时的移动到了Location头部指定的URL上
[303](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/303) | See Other | 表示重定向链接指向的不是新上传的资源，而是另外一个页面
[304](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/304) | Not Modified | 表示无需再次传输请求的内容，即可以使用缓存的内容
[307](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/307) | Temporary Redirect | 请求的资源暂时的移动到了Location头部指向的URL上(302)
[308](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/308) | Permanent Redirect | 请求的资源已经永久移动到了Location头部指定的URL上(301)
<!-- .element: style="font-size: 24px;"--> 

---

### 4xx 客户端响应

表示客户端的请求可能发生了错误，服务器无法正常处理

--

状态码 | 原因短语 | 详细说明
--- | --- | ---
[400](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/400) | Bad Request | 表示由于客户端请求语法无效，服务器无法理解该请求
[401](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/401) | Unauthorized  | 表示由于缺少目标资源要求的身份验证凭证，发送的请求无法处理
402 | Payment Required | 预留，最初的目的是给支付系统使用，但目前并未使用
[403](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/403) | Forbidden | 表示服务器端有能力处理该请求，但是拒绝授权访问
[404](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/404) | Not Found | 表示服务器端无法找到所请求的资源
[405](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/405) | Method Not Allowed | 表示服务器禁止了使用当前HTTP方法的请求(GET和HEAD不包含在内)
[406](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/406) | Not Acceptable | 表示服务器端无法提供与Accept-Charset/Accept-Language消息头相匹配的响应
[407](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/407) | Proxy Authentication Required | 表示缺少代理服务器要求的身份验证凭证，发送的请求无法处理
<!-- .element: style="font-size: 24px;"--> 

--

状态码 | 原因短语 | 详细说明
--- | --- | ---
[408](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/408) | Request Timeout | 表示服务器想要将没有在使用的连接关闭
[409](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/409) | Conflict  | 表示请求与当前服务器端的状态相冲突
[410](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/410) | Gone | 表示请求的内容在服务器上不存在了，同时是永久性的
[411](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/411) | Length Required | 表示由于缺少确定的Content-Length消息头，服务器拒绝客户端的请求
[412](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/412) | Precondition Failed | 表示由于If-Unmodified-Since或If-None-Match消息头的先决条件不成立，请求被服务端拒绝
[413](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/413) | Payload Too Large | 表示请求主体超过了服务器规定的大小，服务器可以选择关闭连接或返回Retry-After首部字段
[414](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/414) | URI Too Long | 表示客户端所请求的URI超过了服务器允许的范围
[415](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/415) | Unsupported Media Type | 表示服务器不支持客户端Content-Type或Content-Encoding头部的格式
<!-- .element: style="font-size: 24px;"--> 

--

状态码 | 原因短语 | 详细说明
--- | --- | ---
[416](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/416) | Range Not Satisfiable | 表示服务器无法处理客户端请求中Range消息头包含的数据区间
[417](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/417) | Expectation Failed | 表示服务器无法满足客户端请求中Expect消息头包含的条件
418 | I'm a teapot | 愚人节彩蛋，[HTCPCP](https://www.wikiwand.com/zh/%E8%B6%85%E6%96%87%E6%9C%AC%E5%92%96%E5%95%A1%E5%A3%B6%E6%8E%A7%E5%88%B6%E5%8D%8F%E8%AE%AE)服务端拒绝用茶壶来冲咖啡
[426](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/426) | Upgrade Required | 表示服务器拒绝处理客户端使用当前协议发送的请求，但可以接受其使用升级后的协议发送的请求
[428](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/428) | Precondition Required | 表示客户端缺少请求的条件，如IF-Match消息头
[429](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/429) | Too Many Requests | 表示在一定的时间内客户端发送了太多的请求，服务端可以用Retry-After消息头来提示客户端等待时长
[431](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/431) | Request Header Fields Too Large | 表示由于请求中的头部字段的值过大，服务器拒绝接受客户端的请求
[451](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/451) | Unavailable For Legal Reasons | 表示服务器由于法律原因，无法提供客户端请求的资源
<!-- .element: style="font-size: 24px;"--> 

---

### 5xx 服务端响应

表示客户端请求有效，但服务器发生错误，无法完成请求

--

状态码 | 原因短语 | 详细说明
--- | --- | ---
[500](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/500) | Internal Server Error | 表示所请求的服务器遇到意外的情况并阻止其执行请求
[501](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/501) | Not Implemented | 表示请求的方法不被服务器支持，因此无法被处理(GET和HEAD除外)
[502](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/502) | Bad Gateway | 表示网关或代理服务器接收到的响应是无效的
[503](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/503) | Service Unavailable | 表示服务器尚未处于可以接受请求的状态
[504](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/504) | Gateway Timeout | 表示网关或代理服务器无法再规定的时间内获得正确的响应
[505](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/505) | HTTP Version Not Supported | 表示服务器不支持请求客户端所使用的HTTP版本
[511](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/511) | Network Authentication Required | 表示客户端需要通过验证才能使用该网络
<!-- .element: style="font-size: 24px;"--> 

---

## 总结

讲了这么多状态码，该怎么使用？

--

1xx状态码，基本不会使用

--

2xx和3xx状态码

![](https://img.zhangchunxin.com/reveal/http/response-code/da105680.png)
<!-- .element: style="height: 550px;"-->

--

4xx状态码

![](https://img.zhangchunxin.com/reveal/http/response-code/5b6f8f21.png)
<!-- .element: style="height: 550px;"-->

--

5xx状态码

![](https://img.zhangchunxin.com/reveal/http/response-code/af6e4e99.png)

---

### 附录

 - [HTTP response codes -MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status)
 - [HTTP状态码 - Wikiwand](https://www.wikiwand.com/zh/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)
 - [TelcoOS 服务RESTful API设计规范 v2.0 - 彭正元&殷一石](http://leanote.zhangchunxin.inhuawei.com/api/file/getAttach?fileId=59cb75afcc9a97f2e600003d)