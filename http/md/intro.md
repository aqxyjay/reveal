# HTTP

**HyperText Transfer Protocol**

[超文本](https://www.wikiwand.com/zh-hans/%E8%B6%85%E6%96%87%E6%9C%AC)传输协议

---

![](https://img.zhangchunxin.com/reveal/http/intro/8376ba09.png)

HTTP是一种Client-Server协议，默认使用80端口，是Web上[各类数据](https://www.wikiwand.com/zh-hans/%E8%B6%85%E5%AA%92%E9%AB%94)交换的基础。

---

# HTTP 连接

--

![](https://img.zhangchunxin.com/reveal/http/intro/70610f1e.png)

---

# HTTP 报文

--

### 请求报文

![](https://img.zhangchunxin.com/reveal/http/intro/a0f0683e.png)

--

### 响应报文

![](https://img.zhangchunxin.com/reveal/http/intro/36503870.png)

---

# HTTP 方法

--

方法 | 说明
--- | ---
GET | 从服务端获取指定的资源
POST | 发送特定类型的数据给服务端，进行资源的创建
PUT | 发送数据给服务端，新增资源或替换目标资源
DELETE | 告诉服务端删除指定的资源

--

方法 | 说明
--- | ---
PATCH | 发送数据给服务端，对资源进行部分修改
OPTIONS | 从服务端获取资源所支持的方法
HEAD | 从服务端获取资源的响应头部，与Get获取到的头部相同
TRACE | 回显服务器收到的请求，主要用于测试或诊断
CONNECT | HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器

---

# HTTP 状态码

--

状态 | 说明
--- | ---
1xx | 消息：请求已被服务器接收，继续处理
2xx | 成功：请求已成功被服务器接收、理解、并接受
3xx | 重定向：需要后续操作才能完成这一请求
4xx | 请求错误：请求含有词法错误或者无法被执行
5xx | 服务器错误：服务器在处理某个正确请求时发生错误

---

# HTTP 版本

--

### HTTP/0.9

1991发布，只有`GET`命令： `GET /index.html`

协议规定，服务端只能响应HTML格式的字符串，不支持别的格式。

```html
<html>
  <body>Hello World</body>
</html>
```

--

### HTTP/1.0

1996年5月，HTTP/1.0 版本发布。

内容大大增加，和我们今天看到的HTTP差别不大。

--

#### 新增特性

 - 支持传输任何格式的内容
 - 引入`POST`和`HEAD`命令
 - 请求/响应格式优化，引入头部信息
 - 增加响应状态码
 - 多字符集支持
 - 多部分发送
 - 权限
 - 缓存
 - 内容编码

--

#### 缺点

每个TCP连接只能发送一个请求 <!-- .element: class="fragment visible"--> 

--

### HTTP/1.1

1997年1月，HTTP/1.1 版本发布。

时至今日，依然是最流行的版本。

--

#### 新增特性

 - 持久链接
 - 管道机制，同一个TCP连接里，客户端发送多个请求
 - `Content-Length`字段
 - 分块传输编码
 - 新增了`PUT`/`PATCH`/`HEAD`/`OPTIONS`/`DELETE`方法
 - 新增了`Host`头部

--

#### 缺点

所有的数据通信是按次序进行的 <!-- .element: class="fragment visible"--> 

--

### HTTP/2

2015年，HTTP/2 发布。

它不叫 HTTP/2.0，因为不会有2.1版本。

下一个版本将是HTTP/3。

--

#### 新增特性

 - 二进制协议
 - 多工(Multiplexing)
 - 数据流
 - 头信息压缩
 - 服务器推送

---

# 基于HTTP的组件系统

![](https://img.zhangchunxin.com/reveal/http/intro/60d54667.png)

--

### Client

用户代理(user-agent)，请求发起者。

 - 浏览器   <!-- .element: class="fragment visible"--> 
 - 爬虫     <!-- .element: class="fragment visible"--> 
 - REST Cient   <!-- .element: class="fragment visible"--> 

--

### Proxy

应用层代理。

 - 缓存(public/private)
 - 过滤(反病毒)
 - 负载均衡
 - 访问控制
 - 登录，存储历史信息

--

### Server

Web服务端，请求的响应者。
![](https://img.zhangchunxin.com/reveal/http/intro/06f60c33.png)

---

## 附录

 - [HTTP概述 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Overview)
 - [超文本传输协议 - Wikiwand](https://www.wikiwand.com/zh-hans/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE)
 - [HTTP 协议入门 - 阮一峰](http://www.ruanyifeng.com/blog/2016/08/http.html)
 - [HTTP协议 - Ken](http://yaochenkun.cn/index.php/2017/07/13/http_article/)