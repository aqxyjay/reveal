
# Quotation marks

---

## 单引号 ' V.S. 双引号 "

--

```javascript
let str1 = 'This is a string with single quotation mark.';
let str2 = "This is a string with double quotation mark.";

console.log(str1);
console.log(str2);
```
<!-- .element: class="fragment visible"-->

```bash
This is a String with single quotation mark.
This is a String with double quotation mark.
```
<!-- .element: class="fragment visible"-->

结论：单独使用都没有任何问题
<!-- .element: class="fragment visible"-->

--

```javascript
let str3 = "<a href='how-to-equal.html' class='url'>How to Equal</a>";
let str4 = "<a href="how-to-equal.html" class="url">How to Equal</a>";

console.log(str3);
console.log(str4);
```
<!-- .element: class="fragment visible"-->

```bash
Uncaught SyntaxError: Unexpected identifier
```
<!-- .element: class="fragment visible"-->

```javascript
let str5 = "<a href='how-to-equal.html' class='url'>How to Equal</a>";
let str6 = "<a href=\"how-to-equal.html\" class=\"url\">How to Equal</a>";

console.log(str5);
console.log(str6);
```
<!-- .element: class="fragment visible"-->

结论：双引号内部可以嵌套单引号，但嵌套双引号，需要转义
<!-- .element: class="fragment visible"-->

--

```javascript
let str7 = '<a href='how-to-equal.html' class='url'>How to Equal</a>';
let str8 = '<a href="how-to-equal.html" class="url">How to Equal</a>';

console.log(str7);
console.log(str8);
```
<!-- .element: class="fragment visible"-->

```bash
Uncaught SyntaxError: Unexpected identifier
```
<!-- .element: class="fragment visible"-->

```javascript
let str9 = '<a href=\'how-to-equal.html\' class=\'url\'>How to Equal</a>';
let str10 = '<a href="how-to-equal.html" class="url">How to Equal</a>';


console.log(str9);
console.log(str10);
```
<!-- .element: class="fragment visible"-->

结论：单引号内部可以嵌套双引号，但嵌套单引号，需要转义
<!-- .element: class="fragment visible"-->

--

### HTML使用的是双引号

```html
<script id="topo_leftTree_top_tpl" type="text/x-handlebars-template">
    <div class="topo_leftTree_div_title" style="display: inline-block;">
        <span class="topo_leftTree_div_icon"></span>
        <span class="topo_leftTree_div_text" title="{{topoManageLabel}}">{{topoManageLabel}}</span> 
    </div>
    <span class="topo_leftTree_div_on"></span>
</script>
```

结论：Javascript中字符串引用HTML时，使用单引号
<!-- .element: class="fragment visible"-->

--

## 总结

 - 单引号在字符串中可以直接引用HTML
 - 单引号可以嵌套双引号字符串
 - 相比双引号，单引号少按一次Shift

*字符串使用单引号优于双引号 —— 方便、省事*

---

### 附录

 - [华为JavaScript语言编程规范 ES5篇2017V1.0](http://w3.huawei.com/ipd/tsl/#!tsl/standard/standard.html?standardId=43549)