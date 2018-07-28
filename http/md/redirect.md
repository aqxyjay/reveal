
# HTTP Redirect

---

## HTTP重定向框架

![](.https://img.zhangchunxin.com/reveal/http/redirect/832fa8e0.png)

---

## HTTP重定向类型

 - 永久重定向
 - 临时重定向
 - 特殊重定向

--

### 永久重定向

原URL不再使用，应该优先选用新的URL

响应码 | 原因短语 | 处理方法 | 典型应用场景
--- | --- | --- | ---
301 | Moved Permanently | GET方法不会发生变更，其他方法*有可能会*变更为GET方法 | 网站重构
308 | Permanent Redirect | 方法和消息主体都*不发生变化* | 网站重构
<!-- .element: style="font-size: 26px;"--> 

--

### 临时重定向

资源无法从其标准地址访问，但可以从另外的地方访问

响应码 | 原因短语 | 处理方法 | 典型应用场景
--- | --- | --- | ---
302 | Found | GET方法不会发生变更，其他方法*有可能会*变更为GET方法 | 由于不可预见的原因该页面暂不可用
303 | See Other | GET方法不会发生变更，其他方法*会变更*为GET方法（消息主体会丢失） | 用于PUT或POST请求完成之后进行页面跳转来防止由于页面刷新导致的操作的重复触发
307 | Temporary Redirect | 方法和消息主体都*不发生变化* | 由于不可预见的原因该页面暂不可用
<!-- .element: style="font-size: 26px;"--> 

--

### 特殊重定向

响应码 | 原因短语 | 典型应用场景
--- | --- | ---
300 | Multiple Choice | 所有的选项在消息主体的 HTML 页面中列出
304 | Not Modified | 缓存值依然有效，可以使用
<!-- .element: style="font-size: 26px;"--> 

---

## 其他重定向方法

 - HTML重定向
 - JavaScript重定向

--

### HTML重定向

```html
<head> 
  <meta http-equiv="refresh" content="0;URL=http://www.example.com/" />
</head>
```

字段 | 说明 | 取值
--- | --- | ---
http-equiv | 改变服务器和用户引擎行为 | refresh(重定向)
content | 重定向的延迟时间和新的URI | 0;URL=http://www.example.com/
<!-- .element: style="font-size: 26px;"--> 

该方法仅适用于HTML页面，并不能应用于图片或者其他类型的内容

--

### JavaScript重定向

```javascript
window.location = "http://www.example.com/";
```

--

### 重定向的优先级

```bash
HTTP > HTML > JavaScript
```

---

## 重定向的使用场景

 - 域名别称
 - 保持链接有效
 - 不安全请求的临时响应
 - 耗时请求的临时响应

--

### 域名别称

场景 | 说明 | 举例
--- | --- | ---
扩大站点的覆盖面 | 将多个域名重定向到主域名上，如缩写、同义词、拼写错误等 | goo.gl -> google.com<br>z00230635.inhuawei.com -> zhangchunxin.inhuawei.com
迁移到另外一个域名 | 公司改名后，你希望用户在搜索旧名称的时候，依然可以访问到应用了新名称的站点 | baidu.com -> google.com
强制使用 HTTPS 协议 | 对于 HTTP 版本站点的请求会被重定向至采用了 HTTPS 协议的版本 | http://google.com -> https://google.com
<!-- .element: style="font-size: 26px;"--> 

--

### 保持链接有效

场景 | 说明 | 举例
--- | --- | ---
重构网站 | 将重构前的URL重定向到重构后的URL | baidu.com/pan/little_movie -> pan.baidu.com/little_movie
<!-- .element: style="font-size: 26px;"--> 

--

### 不安全请求的临时响应

场景 | 说明 | 解决方案
--- | --- | ---
PUT/POST/DELETE请求 | 不安全的请求重复发送后会改变服务端的状态，可能简单点击刷新按钮就会导致请求的重复发送 | 服务器返回一个303响应，含有合适的响应信息，刷新后将不会重复提交
<!-- .element: style="font-size: 26px;"--> 

--

### 耗时请求的临时响应

场景 | 解决方案
--- | ---
耗时较长或优先级较低的请求 | 返回一个 303 (See Other)  重定向响应，该响应链接到一个页面，表示请求的操作已经被列入计划，并且最终会通知用户操作的进展情况，或者允许用户将其取消
<!-- .element: style="font-size: 26px;"--> 

---

### 附录

 - [HTTP 的重定向 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Redirections)