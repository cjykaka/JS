# Generator

## 简介
generator（生成器）是ES6标准引入的新的数据类型。一个generator看上去像一个函数，但可以返回多次。Generator 函数是协程在 ES6 的实现，
最大特点就是可以交出函数的执行权（即暂停执行）。
## 句法
```javascript
function* gen(x){
      var y = yield x + 2;
      return y;
    }
```
上面代码就是一个 Generator 函数。它不同于普通函数，是可以暂停执行的，所以函数名之前要加星号，以示区别。
## 方法
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

