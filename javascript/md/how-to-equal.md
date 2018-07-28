
# How to Equal in JavaScript

---

## `===` 严格相等
## `==` 宽松相等
## `Object.is` (ES6新增)

---

## === V.S. ==

--

### True or False

```javascript
let num = 0;
let obj = new String("0");
let str = "0";

console.log(num === num);
console.log(num == num);
console.log(obj === obj);
console.log(obj == obj);
console.log(str === str);
console.log(str == str);

console.log(num === obj);
console.log(num == obj);
console.log(num === str);
console.log(num == str);
console.log(obj === str);
console.log(obj == str);
console.log(null === undefined);
console.log(null == undefined);
console.log(obj === null);
console.log(obj == null);
console.log(obj === undefined);
console.log(obj == undefined);

```

--

### ===

 - 类型相同，值也相同，返回true
 - 不会进行隐式转换，类型不同则返回false

--

### ==

 - 比较前将值转换为同一类型
 - 转换后，如果值相同，返回true

---

## === V.S. Object.is

--

### True or False

```javascript
let num1 = +0;
let num2 = -0;
let num3 = 0;
let nan = NaN;

console.log(num1 === num1);
console.log(Object.is(num1, num1));
console.log(num2 === num2);
console.log(Object.is(num2, num2));
console.log(num3 === num3);
console.log(Object.is(num3, num3));
console.log(nan === nan);
console.log(Object.is(nan, nan));

console.log(num1 === num2);
console.log(Object.is(num1, num2));
console.log(num1 === num3);
console.log(Object.is(num1, num3));
console.log(num2 === num3);
console.log(Object.is(num2, num3));
console.log(nan === num2/num1);
console.log(Object.is(nan, num2/num1));
```

--

### Object.is

 - 区分`+0`和`-0`，两者比较返回false
 - 对NaN进行比较，同为NaN时返回true

--

### ===

 - 不区分`+0`和`-0`，两者比较返回true
 - 任何值与NaN比较，都返回false
 
*两者只有在number类型的0值和NaN场景下才有区别。*

---

## 总结

 - `==`，比较前会进行隐式转换，容易产生误判，造成Bug
 - `Object.is`，满足全部场景，但需要ES6支持，兼容性一般
 - `===`，能够满足绝大部分常用场景，支持全部浏览器，兼容性最好，推荐使用

--

### 额外说明

--

```javascript
let obj = new String("0");
let str = "0";

console.log(obj === str); //false
console.log(obj == str); //true

typeof obj; //"object"
typeof str; //"string"
```

`obj`是一种装箱对象，而`str`是字符串原始类型

--

以上所有对==和===的说明

均适用于!=和!==

---

### 附录

 - [JavaScript 中的相等性判断 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Equality_comparisons_and_sameness)
 - [JavaScript Equality Table - Dorey - Github](http://dorey.github.io/JavaScript-Equality-Table)
 - [Why does (“foo” === new String(“foo”)) evaluate to false in JavaScript? - Stackoverflow](https://stackoverflow.com/questions/10951906/why-does-foo-new-stringfoo-evaluate-to-false-in-javascript)