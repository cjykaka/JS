# Generator

## 一、简介
generator（生成器）是ES6标准引入的新的数据类型。一个generator看上去像一个函数，但可以返回多次。Generator 函数是协程在 ES6 的实现，
最大特点就是可以交出函数的执行权（即暂停执行）。
## 二、句法
```javascript
function* gen(x){
      var y = yield x + 2;
      return y;
    }
```
上面代码就是一个 Generator 函数。它不同于普通函数，是可以暂停执行的，所以函数名之前要加星号，以示区别。
## 三、方法
 1. 调用generator对象有两个方法，第一种就是不断地调用generator对象的next()方法：
 ```javascript
 var g = gen(1);
    g.next() // { value: 3, done: false }
    g.next() // { value: undefined, done: true }
```
next()方法会执行generator的代码，然后，每次遇到yield x;就返回一个对象{value: x, done: true/false}，然后“暂停”。返回的value就是yield的返回值，
done表示这个generator是否已经执行结束了。如果done为true，则value就是return的返回值。当执行到done为true时，这个generator对象就已经全部执行完毕，
不要再继续调用next()了。

2. 第二种就是直接用for ... of循环迭代generator对象，这种方式不需要我们自己判断done：
```javascript
for (var x of gen(1)) {
    console.log(x); // 输出3
}
```

3. next 方法还可以接受参数，这是向 Generator 函数体内输入数据:
```javascript
function* gen() {
  while(true) {
    var value = yield null;
    console.log(value);
  }
}

var g = gen();
g.next(1); 
// "{ value: null, done: false }"
g.next(2); 
// "{ value: null, done: false }"
// 2
```

4. generator.return：
```javascript
function* gen() { 
  yield 1;
  yield 2;
  yield 3;
}

var g = gen();

g.next();        // { value: 1, done: false }
g.return('foo'); // { value: "foo", done: true }
g.next();        // { value: undefined, done: true }
```
以上示例显示了一个简单的生成器和返回方法；

```javascript
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

var g = gen();
g.next(); // { value: 1, done: false }
g.next(); // { value: 2, done: false }
g.next(); // { value: 3, done: false }
g.next(); // { value: undefined, done: true }
g.return(); // { value: undefined, done: true }
g.return(1); // { value: 1, done: true }
```
如果没有提供参数，则返回对象与.next（）相同; 如果提供了一个参数，它将被设置为返回对象的value属性的值。

5. generator.throw
```javascript
function* gen() {
  while(true) {
    try {
       yield 42;
    } catch(e) {
      console.log('Error caught!');
    }
  }
}

var g = gen();
g.next();
// { value: 42, done: false }
g.throw(new Error('Something went wrong'));
// "Error caught!"
// { value: 42, done: false }
```
以上示例显示了一个简单的生成器和使用throw方法抛出的错误。 一个错误可以像往常一样被try ... catch块捕获。这对于异步编程无疑是很重要的。



# Async
## 一、简介
一句话，async 函数就是 Generator 函数的语法糖。
## 二、async 函数的优点
async 函数对 Generator 函数的改进，体现在以下三点。

* 内置执行器。 Generator 函数的执行必须靠执行器，所以才有了 co 函数库，而 async 函数自带执行器。也就是说，async 函数的执行，与普通函数一模一样，只要一行。

```javascript
    var result = asyncReadFile();
```
* 更好的语义。 async 和 await，比起星号和 yield，语义更清楚了。async 表示函数里有异步操作，await 表示紧跟在后面的表达式需要等待结果。

* 更广的适用性。 co 函数库约定，yield 命令后面只能是 Thunk 函数或 Promise 对象，而 async 函数的 await 命令后面，可以跟 Promise 对象和原始类型的值（数值、字符
  串和布尔值，但这时等同于同步操作）。
## 三、async函数的实现
async 函数的实现，就是将 Generator 函数和自动执行器，包装在一个函数里。
```javascript

    async function fn(args){
      // ...
    }

    // 等同于

    function fn(args){ 
      return spawn(function*() {
        // ...
      }); 
    }
```
所有的 async 函数都可以写成上面的第二种形式，其中的 spawn 函数就是自动执行器。
## 四、async 函数的用法
同 Generator 函数一样，async 函数返回一个 Promise 对象，可以使用 then 方法添加回调函数。当函数执行的时候，一旦遇到 await 就会先返回，等到触发的异步操作完成，再接
着执行函数体内后面的语句。
下面是一个例子。
```javascript
    async function getStockPriceByName(name) {
      var symbol = await getStockSymbol(name);
      var stockPrice = await getStockPrice(symbol);
      return stockPrice;
    }

    getStockPriceByName('goog').then(function (result){
      console.log(result);
    });
```
上面代码是一个获取股票报价的函数，函数前面的async关键字，表明该函数内部有异步操作。调用该函数时，会立即返回一个Promise对象。

下面的例子，指定多少毫秒后输出一个值。
```javascript
    function timeout(ms) {
      return new Promise((resolve) => {
        setTimeout(resolve, ms);
      });
    }

    async function asyncPrint(value, ms) {
      await timeout(ms);
      console.log(value)
    }

    asyncPrint('hello world', 50);
```
上面代码指定50毫秒以后，输出"hello world"。
## 六、注意点
await 命令后面的 Promise 对象，运行结果可能是 rejected，所以最好把 await 命令放在 try...catch 代码块中。
```javascript
    async function myFunction() {
      try {
        await somethingThatReturnsAPromise();
      } catch (err) {
        console.log(err);
      }
    }

    // 另一种写法

    async function myFunction() {
      await somethingThatReturnsAPromise().catch(function (err){
        console.log(err);
      });
    }
```
await 命令只能用在 async 函数之中，如果用在普通函数，就会报错。
```javascript
    async function dbFuc(db) {
      let docs = [{}, {}, {}];

      // 报错
      docs.forEach(function (doc) {
        await db.post(doc);
      });
    }
```
上面代码会报错，因为 await 用在普通函数之中了。但是，如果将 forEach 方法的参数改成 async 函数，也有问题。
```javascript
    async function dbFuc(db) {
      let docs = [{}, {}, {}];

      // 可能得到错误结果
      docs.forEach(async function (doc) {
        await db.post(doc);
      });
    }
```
上面代码可能不会正常工作，原因是这时三个 db.post 操作将是并发执行，也就是同时执行，而不是继发执行。正确的写法是采用 for 循环。
```javascript
    async function dbFuc(db) {
      let docs = [{}, {}, {}];

      for (let doc of docs) {
        await db.post(doc);
      }
    }
```
如果确实希望多个请求并发执行，可以使用 Promise.all 方法。
```javascript
    async function dbFuc(db) {
      let docs = [{}, {}, {}];
      let promises = docs.map((doc) => db.post(doc));

      let results = await Promise.all(promises);
      console.log(results);
    }

    // 或者使用下面的写法

    async function dbFuc(db) {
      let docs = [{}, {}, {}];
      let promises = docs.map((doc) => db.post(doc));

      let results = [];
      for (let promise of promises) {
        results.push(await promise);
      }
      console.log(results);
    }
```


# Reflect
## 一、简介
Reflect不是构造函数， 要使用的时候直接通过Reflect.method()调用， Reflect有的方法和Proxy差不多， 而且多数Reflect方法原生的Object已经重新实现了。
## 二、方法
1. Reflect.get
Reflect.get方法允许您获取对象上的属性。
```javascript
// Object
var obj = { x: 1, y: 2 };
Reflect.get(obj, 'x'); // 1

// Array
Reflect.get(['zero', 'one'], 1); // "one"

// Proxy with a get handler
// Proxy with a get handler
var x = {p: 1};
var obj = new Proxy(x, {
  get(t, k, r) { return k + 'bar'; }
});
Reflect.get(obj, 'foo'); // "foobar"
```
2. Reflect.set
Reflect.set方法允许设置对象上的属性,能给属性赋值。
```javascript
// Object
var obj = {};
Reflect.set(obj, 'prop', 'value'); // true
obj.prop; // "value"

// Array
var arr = ['duck', 'duck', 'duck'];
Reflect.set(arr, 2, 'goose'); // true
arr[2]; // "goose"

// It can truncate an array.
Reflect.set(arr, 'length', 1); // true
arr; // ["duck"]; 
```
3. Reflect.apply
用于反射调用函数并传参
语法：
```javascript
Reflect.apply(target, thisArgument, argumentsList)
```
* target:目标函数
* thisArgument:目标对象，用于绑定函数上下文中的this 
* argumentsList:可迭代的参数列表

```javascript
Reflect.apply(Math.floor, undefined, [1.75]); 
// 1;

Reflect.apply(String.fromCharCode, undefined, [104, 101, 108, 108, 111]);
// "hello"

Reflect.apply(RegExp.prototype.exec, /ab/, ['confabulation']).index;
// 4

Reflect.apply(''.charAt, 'ponies', [3]);
// "i"
```
4.Reflect.has


  