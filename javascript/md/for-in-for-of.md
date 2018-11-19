
# for...in...<br>and<br>for...of...

---

### for...of...

--

```javascript
let name = 'Harry';
let animals = ['🐔', '🐷', '🐑', '🐇'];
let animalSet = new Set(animals);
let car = {
  make: 'VW',
  model: 'Golf',
  year: '1996'
};
```

--

```javascript
let name = 'Harry';

for(let i of name){
    console.log(i);
}
```
```text
H
a
r
r
y
```
<!-- .element: class="fragment visible"-->

--

```javascript
let animals = ['🐔', '🐷', '🐑', '🐇'];

for(let i of animals) {
    console.log(i);
}
```
```text
🐔
🐷
🐑
🐇
```
<!-- .element: class="fragment visible"-->

--

```javascript
let animals = ['🐔', '🐷', '🐑', '🐇'];
let animalSet = new Set(animals);

for (let i of animalSet) {
    console.log(i);
}
```
```text
🐔
🐷
🐑
🐇
```
<!-- .element: class="fragment visible"-->

--

```javascript
let car = {
  make: 'VW',
  model: 'Golf',
  year: '1996'
};

for(let i of car){
    console.log(i);
}
```
```text
Uncaught TypeError: car is not iterable
```
<!-- .element: class="fragment visible"-->

--

*for...of...*

循环一个**可迭代的对象**

Array
String
Map
Set
Arguments

---

### for...in...

--

```javascript
let name = 'Harry';
let animals = ['🐔', '🐷', '🐑', '🐇'];
let car = {
  make: 'VW',
  model: 'Golf',
  year: '1996'
};
```

--

```javascript
let name = 'Harry';

for(let i in name){
    console.log(i);
    console.log(name[i]);
}
```
```text
0
H
1
a
2
r
3
r
4
y
```
<!-- .element: class="fragment visible"-->

--

```javascript
let animals = ['🐔', '🐷', '🐑', '🐇'];

for(let i in animals) {
    console.log(i);
    console.log(animals[i]);
}
```
```text
0
🐔
1
🐷
2
🐑
3
🐇
```
<!-- .element: class="fragment visible"-->

--

```javascript
let car = {
  make: 'VW',
  model: 'Golf',
  year: '1996'
};

for(let i in car){
    console.log(i);
    console.log(car[i]);
}
```
```text
make
VW
model
Golf
year
1996
```
<!-- .element: class="fragment visible"-->

--

```javascript
let animals = ['🐔', '🐷', '🐑', '🐇'];
let animalSet = new Set(animals);

for (let i in animalSet) {
    console.log(i);
}
```
```text
undefined
```
<!-- .element: class="fragment visible"-->

--

*for...in...*

循环一个**对象**所有可枚举的**属性**

Object

---

## 附录

 - [循环和迭代 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Loops_and_iteration)
 - [深入了解 JavaScript 中的 for 循环 - 编译青春](https://funteas.com/topic/5a14e5dba8355d3c2270f548)
