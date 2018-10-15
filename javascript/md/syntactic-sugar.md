
# JavaScript<br>Array<br>语法糖

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
Array.of()
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
Array.from()
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

---

### 判断是否为Array

```javascript
// deprecated
let array = new Array();
array instanceof Array;
```
<!-- .element: class="fragment visible"-->

--

```javascript
Array.isArray();
```

确定传递的值是否是一个 Array。
<!-- .element: class="fragment visible"-->

--

```javascript
/ 下面的函数调用都返回 true
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

