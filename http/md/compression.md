
# HTTP Compression
<!-- .element: style="font-size: 120px;"-->

--

数据压缩是提高 Web 站点性能的一种重要手段

对于有些文件来说，压缩比率可以高达70%，从而大大减低对于带宽的需求

详见：[具体压缩算法列表](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Encoding#%E6%8C%87%E4%BB%A4)

---

## 端到端压缩

消息体压缩是在服务器端完成的，并且在传输过程中保持不变，直到抵达客户端

--

### 示意图

![](https://img.zhangchunxin.com/reveal/http/compression/d723fb2a.png)

--

### 压缩协商

![](https://img.zhangchunxin.com/reveal/http/compression/d6ccf878.png)

--

#### Accept-Encoding: identity

```http
GET /api/negotiation/employee/00230635
Accept: application/json
Accept-Language: zh_CN
Accept-Encoding: identity
Accept-Charset: utf-8
```
<!-- .element: class="fragment visible"--> 

```http
HTTP/1.1 200 
Content-Encoding: identity
Content-Language: en_US
Content-Type: application/json;charset=utf-8
Content-Length: 67
Date: Wed, 17 Jan 2018 09:15:20 GMT

{"status":"success","data":{"id":"00230635","name":"zhangchunxin"}}
```
<!-- .element: class="fragment visible"--> 

--

#### Accept-Encoding: gzip

```http
GET /api/negotiation/employee/00230635
Accept: application/json
Accept-Language: zh_CN
Accept-Encoding: gzip
Accept-Charset: utf-8
```
<!-- .element: class="fragment visible"--> 

```http
Content-Encoding: gzip
Content-Language: en_US
Content-Length: 83
Content-Type: application/json;charset=utf-8
Date: Wed, 17 Jan 2018 09:17:52 GMT

{"status":"success","data":{"id":"00230635","name":"zhangchunxin"}}
```
<!-- .element: class="fragment visible"--> 

---

## 逐跳压缩

逐跳压缩不通过源头服务器进行压缩

是对客户端与服务器之间的任意两个节点之间传递的消息主题的压缩

--

### 示意图

![](https://img.zhangchunxin.com/reveal/http/compression/17adbc20.png)

--

### 压缩协商

![](https://img.zhangchunxin.com/reveal/http/compression/762e1566.png)

头部 | 类型 | 含义
--- | --- | ---
TE | 请求头 | 指定节点希望使用的传输编码类型
Transfer-Encoding | 响应头 | 表示传输所采用的编码形式
<!-- .element: style="font-size: 24px;"-->

---

### 附录

- [HTTP 协议中的数据压缩](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Compression)