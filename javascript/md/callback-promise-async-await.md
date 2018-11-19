
# Callback<br>to<br>Promise<br>to<br>Async/Await

---

## Callback

Javascript的方法也是一种对象，可以作为参数传递给另一个方法(函数)。
<br>
这时，我们就叫它回调方法。

--

```javascript
function print(num){
	console.log(num);
}

function add(num1, num2, callback){
	var sum = num1 + num2;
	callback(sum);
}

add(1, 2, print);
```
```text
3
```
<!-- .element: class="fragment visible"--> 

--

```javascript
fs.readdir(source, function (err, files) {
    if (err) {
        console.log('Error finding files: ' + err);
    } else {
        files.forEach(function (filename, fileIndex) {
            gm(source + filename).size(function (err, values) {
                if (err) {
                    console.log('Error identifying file size: ' + err);
                } else {
                    aspect = (values.width / values.height);
                    widths.forEach(function (width, widthIndex) {
                        height = Math.round(width / aspect);
                        this.resize(width, height).write(dest + 'w' + width + '_' + filename, function (err) {
                            if (err) console.log('Error writing file: ' + err);
                        });
                    }.bind(this));
                }
            });
        });
    }
});
```

Callback Hell
<!-- .element: class="fragment visible"--> 

---

## Promise

Promise是ES6定义的一种**对象**。

--

### Promise的构造函数

```javascript
let promise = new Promise(function(resolve, reject) {
    // 异步处理
    // 处理结束后，调用resolve或reject改变状态
});
```
`resolve`和`reject`均为可选参数。

--

### Promise的状态

 - Fulfilled：表示Promise得到满足，如调用成功
 - Rejected：表示Promise没有得到满足，如发生异常
 - Pending：表示Promise处于初始化状态

![](https://img.zhangchunxin.com/reveal/javascript/callback-promise-async-await/promise-states.png)

--

### Promise的链式流程

```javascript
function taskA() {
    // do something
    console.log("Task A");
}

function taskB() {
    // do something
    console.log("Task B");
}

function onRejected(error) {
    console.log("Catch Error: A or B", error);
}

function finalTask() {
    console.log("Final Task");
}

let promise = Promise.resolve();
promise
    .then(taskA)
    .then(taskB)
    .catch(onRejected)
    .then(finalTask);
```

 - `Promise.resolve()`：new Promise() 方法的快捷方式
 - `then`：Fulfilled时的回调方法
 - `catch`：Rejected时的回调方法

--

![](https://img.zhangchunxin.com/reveal/javascript/callback-promise-async-await/promise-then-catch-flow.png)

--

### Promise的链式传参

```javascript
function doubleUp(value) {
    return value * 2;
}

function increment(value) {
    return value + 1;
}

function output(value) {
    console.log(value);
}

let promise = Promise.resolve(1);
promise
    .then(increment)
    .then(doubleUp)
    .then(output)
    .catch(function(error){
        // promise chain中出现异常的时候会被调用
        console.error(error);
    });
```

--

### Promise和数组

--

**Promise.all(promiseArray)**

 - `promiseArray`：Promise对象组成的数组

当`promiseArray`中**全部**的对象的状态都变为**Resolved**时，会返回一个新的Promise，并且使用`promiseArray`中**全部对象的值**进行resolve。

当`promiseArray`中**任一**对象的状态变为**Rejected**时，则整个`Promise.all`调用停止，并使用这个Promise的值进行reject。

--

```javascript
let p1 = Promise.resolve(1),
    p2 = Promise.resolve(2),
    p3 = Promise.resolve(3);
Promise.all([p1, p2, p3])
    .then(function (results) {
        console.log(results);
    }).catch(function(error) {
        console.error(error);
    });
```

--

```javascript
function timerPromise(delay) {
    return new Promise(function (resolve) {
        setTimeout(function () {
            resolve(delay);
        }, delay);
    });
}
var startDate = Date.now();

Promise.all([
    timerPromise(1),
    timerPromise(32),
    timerPromise(64),
    timerPromise(128)
]).then(function (values) {
    console.log(Date.now() - startDate + 'ms');
    console.log(values);
});
```

--

#### **`Promise.all`**的特性

 - `promiseArray`数组中的调用会同时并行执行
 - 每个Promise的结果，与`promiseArray`数组的顺序是一致的

--

**Promise.race(promiseArray)**

 - `promiseArray`：Promise对象组成的数组

当`promiseArray`中**任一**对象的状态变为**Resolved**或**Rejected**时，则整个`Promise.race`调用停止，并使用这个Promise的值进行resolve或reject。。

--

```javascript
function timerPromise(delay) {
    return new Promise(function (resolve) {
        setTimeout(function () {
            resolve(delay);
        }, delay);
    });
}
var startDate = Date.now();

Promise.race([
    timerPromise(1),
    timerPromise(32),
    timerPromise(64),
    timerPromise(128)
]).then(function (values) {
    console.log(Date.now() - startDate + 'ms');
    console.log(values);
});
```

---

## Async/Await

---

## 附录

 - [JavaScript回调函数 - dandananddada](https://cnodejs.org/topic/564dd2881ba2ef107f854e0b)
 - [Callback Hell](http://callbackhell.com/)
 - [JavaScript Promise迷你书](http://liubin.org/promises-book/)
 - [异步 JavaScript 的演化史：从回调到 Promise 再到 Async/Await](https://www.infoq.cn/article/JQxzWt7FqDc9p7jJ_1hs)
