
# JavaScript<br>Array<br>语法糖

---

类型 | 命令
--- | ---
初始化 | [Array.of](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/of)
转换为数组 | [Array.from](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
判断是否为数组 | [Array.isArray](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)
数组填充 | [Array.prototype.fill](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)
多个数组合并 | [Array.prototype.concat](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)
过滤满足条件的元素 | [Array.prototype.filter](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
验证数组元素是否全部满足条件 | [Array.prototype.every](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
验证数组元素是否部分满足条件 | [Array.prototype.some](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
倒序排序 | [Array.prototype.reverse](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)
根据条件排序 | [Array.prototype.sort](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
查找数组元素 | [Array.prototype.find](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/find)<br>[Array.prototype.findIndex](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)<br>[Array.prototype.indexOf](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)<br>[Array.prototype.lastIndexOf](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf)
数组是否包含某元素 | [Array.prototype.includes](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)
处理数组的元素 | [Array.prototype.map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
分割数组 | [Array.prototype.slice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
数组元素增删改 | [Array.prototype.splice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
队列操作 | [Array.prototype.pop](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)<br>[Array.prototype.push](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push)<br>[Array.prototype.shift](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)<br>[Array.prototype.unshift](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)
数组简化 |  [Array.prototype.reduce](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)<br>[Array.prototype.reduceRight](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight)
<!-- .element: style="font-size: 16px;"-->

---

### 初始化

```javascript
let array1 = ['a', 'b'];
let array2 = new Array('a', 'b');
let array3 = new Array(2);
```
<!-- .element: class="fragment visible"-->

--

```javascript
Array.of(element0[, element1[, ...[, elementN]]])
```

创建一个具有可变数量参数的新数组实例，不限制参数的数量或类型
<!-- .element: class="fragment visible"-->

--

```javascript
Array.of(1);         // [1]
Array.of(1, 2, 3);   // [1, 2, 3]
Array.of('a', 'b', 'c');   // ["a", "b", "c"]
Array.of(undefined); // [undefined]
```

---

### 转换为数组

```javascript
// deprecated
let s = new Set(['foo', window]);
let array = [];
s.forEach(ele => array.push(ele));
```
<!-- .element: class="fragment visible"-->

--

```javascript
Array.from(arrayLike[, mapFn[, thisArg]])
```

从一个类似数组或可迭代对象中创建一个新的数组实例。
<!-- .element: class="fragment visible"-->

--

```javascript
Array.from('foo'); 
// ["f", "o", "o"]
let s = new Set(['foo', window]); 
Array.from(s); 
// ["foo", window] 
let m = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(m); 
// [[1, 2], [2, 4], [4, 8]]
```

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-from.html" height="490" frameborder="0" width="100%"></iframe>

---

### 判断是否为数组

```javascript
// deprecated
let array = new Array();
array instanceof Array;
```
<!-- .element: class="fragment visible"-->

--

```javascript
Array.isArray(obj)
```

确定传递的值是否是一个 Array。
<!-- .element: class="fragment visible"-->

--

```javascript
// 下面的函数调用都返回 true
Array.isArray([]);
Array.isArray([1]);
Array.isArray(new Array());
// 鲜为人知的事实：其实 Array.prototype 也是一个数组。
Array.isArray(Array.prototype); 

// 下面的函数调用都返回 false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(17);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
Array.isArray({ __proto__: Array.prototype });
```

---

### 数组填充

```javascript
Array.prototype.fill(value[, start[, end]])
```
<!-- .element: class="fragment visible"-->

用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-fill.html" height="490" frameborder="0" width="100%"></iframe>

---

### 多个数组合并

```javascript
Array.prototype.concat(value1[, value2[, ...[, valueN]]])
```
<!-- .element: class="fragment visible"-->

合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-concat.html" height="490" frameborder="0" width="100%"></iframe>

---

### 过滤满足条件的元素

```javascript
Array.prototype.filter(callback(element[, index[, array]])[, thisArg])
```
<!-- .element: class="fragment visible"-->

创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-filter.html" height="490" frameborder="0" width="100%"></iframe>

---

### 验证数组元素是否全部满足条件

```javascript
Array.prototype.every(callback[, thisArg])
```
<!-- .element: class="fragment visible"-->

测试数组的所有元素是否都通过了指定函数的测试。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-every.html" height="490" frameborder="0" width="100%"></iframe>

---

### 验证数组元素是否部分满足条件

```javascript
Array.prototype.some(callback[, thisArg])
```
<!-- .element: class="fragment visible"-->

测试数组的某些元素是否都通过了指定函数的测试。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-some.html" height="490" frameborder="0" width="100%"></iframe>

---

### 倒序排序

```javascript
Array.prototype.reverse()
```
<!-- .element: class="fragment visible"-->

将数组中元素的位置颠倒。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-reverse.html" height="490" frameborder="0" width="100%"></iframe>

---

### 根据条件排序

```javascript
Array.prototype.sort([compareFunction])
```
<!-- .element: class="fragment visible"-->

用原地算法对数组的元素进行排序，并返回数组。默认排序顺序是根据字符串Unicode码点。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-sort.html" height="490" frameborder="0" width="100%"></iframe>

---

### 查找数组元素

```javascript
Array.prototype.find(callback[, thisArg])
//返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined。
Array.prototype.findIndex(callback[, thisArg])
//返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1。
Array.prototype.indexOf(searchElement[, fromIndex = 0])
//返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。
Array.prototype.lastIndexOf(searchElement[, fromIndex = arr.length - 1])
//返回指定元素在数组中的最后一个的索引，如果不存在则返回 -1。
```
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-find.html" height="490" frameborder="0" width="100%"></iframe>

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-findindex.html" height="490" frameborder="0" width="100%"></iframe>

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-indexof.html" height="490" frameborder="0" width="100%"></iframe>

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-lastindexof.html" height="490" frameborder="0" width="100%"></iframe>

---

### 数组是否包含某元素

```javascript
Array.prototype.includes(searchElement[, fromIndex = 0])
```
<!-- .element: class="fragment visible"-->

判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-includes.html" height="490" frameborder="0" width="100%"></iframe>

---

### 处理数组的元素

```javascript
Array.prototype.map(callback(currentValue[, index[, array]])[, thisArg])
```
<!-- .element: class="fragment visible"-->

创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-map.html" height="490" frameborder="0" width="100%"></iframe>

---

### 分割数组

```javascript
Array.prototype.slice([begin[, end]])
```
<!-- .element: class="fragment visible"-->

返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝到一个新数组对象。且原始数组不会被修改。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-slice.html" height="490" frameborder="0" width="100%"></iframe>

---

### 数组元素增删改

```javascript
Array.prototype.splice(start[, deleteCount[, item1[, item2[, ...]]]])
```
<!-- .element: class="fragment visible"-->

返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝到一个新数组对象。且原始数组不会被修改。
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-splice.html" height="490" frameborder="0" width="100%"></iframe>

---

### 队列操作

```javascript
Array.prototype.pop()
//从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。
Array.prototype.push(element1[, ..., elementN])
//将一个或多个元素添加到数组的末尾，并返回该数组的新长度。
Array.prototype.shift()
//从数组中删除第一个元素，并返回该元素的值。此方法更改数组的长度。
Array.prototype.unshift(element1[, ..., elementN])
//将一个或多个元素添加到数组的开头，并返回该数组的新长度。
```
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-pop.html" height="490" frameborder="0" width="100%"></iframe>

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-push.html" height="490" frameborder="0" width="100%"></iframe>

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-shift.html" height="490" frameborder="0" width="100%"></iframe>

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-unshift.html" height="490" frameborder="0" width="100%"></iframe>

---

### 数组简化

```javascript
Array.prototype.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])
//对累计器和数组中的每个元素（从左到右）应用一个函数，将其简化为单个值。
Array.prototype.reduceRight(callback(accumulator, currentValue[, index[, array]])[, initialValue])
//对累计器和数组中的每个元素（从右到左）应用一个函数，将其简化为单个值。
```
<!-- .element: class="fragment visible"-->

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-reduce.html" height="490" frameborder="0" width="100%"></iframe>

--

<iframe src="https://interactive-examples.mdn.mozilla.net/pages/js/array-reduce-right.html" height="490" frameborder="0" width="100%"></iframe>

---

## 练习

```javascript
let array = [[1, 2], [3, 4], [4, 5], [2, 1], [7, 6]];
// TODO your code here...
console.log(array);
```

期待输出：
```javascript
[6, 7]
```

--

提示：
1. 简化为一维数组
2. 去重
3. 根据条件过滤
4. 排序

---

## 附录

 - [Array - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)
