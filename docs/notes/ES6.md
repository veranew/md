:heart: one today is worth two tomorrows. :heart:

# let&const

## var
es6之前我们都是用var来声明变量

```js
var a = 1
```
但==var声明变量有一些特点和弊端==：
**1. `var`的作用域仅有函数作用域和全局作用域。不支持块级作用域。容易造成作用域污染问题。**
```js
for (var i = 0; i < 3; i++) {
  console.log(i); // 分别打印 0 1 2
}
console.log(i) // 3  在循环体的外面还是可以读到i
```
为了不声明到全局上，我们让上面代码做一个自执行
```js
(function () {
  for (var i = 0; i < 3; i++) {
    console.log(i);
  }
})()
console.log(i); // ReferenceError: i is not defined  这样就不会污染了
```
另外还有个问题
```js
// 我们希望每一秒打印出i
for (var i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log(i); // 结果是打印出3 3 3, 因为js会先执行同步代码，再执行异步代码，等到异步代码的时候，i已经都变成了全局的3.所以打印结果不是我们想要的
  })
}
console.log(i) // 3
```
为了解决这个问题，我们还是得换成函数，加一个作用域
```js
for (var i = 0; i < 3; i++) {
  (function (i) {
    setTimeout(function () {
      console.log(i); // 0 1 2
    }, 1000)
  })(i)
}
console.log(i); // 3
```
**2. `var`的变量提升问题**
用var声明的变量存在变量提升，也就是在声明之前取值不报错，可以得到undefined，不太符合我们的逻辑，也容易出错，加大排查错误难度。
```js
// var 的情况
typeof a; // // 输出 undefined
console.log(a); // 输出 undefined
var a= 2;

```

**3. `var`允许重复声明**
```js
var a  = 1;
var a = 2;
console.log(a) // 2
```
## let
为了解决以上问题，ES6出了新的声明方式 `let`， 具有以下特点：
**1. 块级作用域**
`let` 所声明的变量，只在`let`命令所在的代码块内有效。
```js
// 一个花括号{}就是一个代码块
{
  let a = 10;
  var b = 1;
}

console.log(a) // ReferenceError: a is not defined.
console.log(b) // 1
```
for循环非常适合用`let`，计数器仅在循环体内有效。并且配合定时器，也不会出现上面那种不符合预期的情况。
```js
for (let i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log(i); // 0 1 2
  }, 1000)
}
console.log(i); // ReferenceError: i is not defined
```
另外，for循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。
```js
// 函数内部的变量i与循环变量i不在同一个作用域，有各自单独的作用域。
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}
// abc
// abc
// abc
```
**2. 不存在变量提升**
在`let`声明之前，变量不存在，如果使用会报错。
```js
// let 的情况
console.log(b); // 报错 ReferenceError
let b= 2;
```
值得注意的是==暂时性死区(temporal dead zone，简称 TDZ)==问题。只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

总之，在代码块内，使用`let`命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。
```js
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```
“暂时性死区”也意味着`typeof`不再是一个百分之百安全的操作。
```js
typeof x; // ReferenceError
let x;
```
作为比较，如果一个变量根本没有被声明，使用`typeof`反而不会报错。
```js
typeof undeclared_variable // "undefined"
```
这样的设计是为了让大家养成良好的编程习惯，变量一定要在声明之后使用，否则就报错。ES6 规定暂时性死区和let、const语句不出现变量提升，主要是为了减少运行时错误，防止在变量声明前就使用这个变量，从而导致意料之外的行为。这样的错误在 ES5 是很常见的，现在有了这种规定，避免此类错误就很容易了。
```js
// 注意函数的参数
function bar(x = y, y = 2) {
  return [x, y];
}

bar(); // 报错
```
```js
// 不报错
var x = x;

// 报错
let x = x;
// ReferenceError: x is not defined
```
**3. 不允许重复声明**

`let`不允许在相同作用域内，重复声明同一个变量。
```js
// 报错
function func() {
  let a = 10;
  var a = 1;
}

// 报错
function func() {
  let a = 10;
  let a = 1;
}
```
## const
`const`表示声明只读变量。一旦声明不可改变。所以`const`声明之后必须立即赋值，否则会报错。
```js
const a; // SyntaxError: Missing initializer in const declaration
```
==注意：==
`const`声明保证内存地址不可更改。对于简单数据类型，`const`保存是值，但对于复杂数据类型，`const`保存的实际是一个指针，但指针所指向的对象是可以更改的。如果想将数据对象冻结，需要使用`Object.freeze()`方法。
```js
const foo = Object.freeze({});

// 常规模式时，下面一行不起作用；
// 严格模式时，该行会报错
foo.prop = 123;
```
除了将对象本身冻结，对象的属性也应该冻结。下面是一个将对象彻底冻结的函数。
```js
var constantize = (obj) => {
  Object.freeze(obj);
  Object.keys(obj).forEach( (key, i) => {
    if ( typeof obj[key] === 'object' ) {
      constantize( obj[key] );
    }
  });
};
```
`const`同样具有块级作用域、不允许变量提升、不允许重复声明等特点。参考以上`let`部分。

参考：
[let](https://wangdoc.com/es6/let.html)

# 解构赋值

# 模板字符串

# 箭头函数

# 展开运算符

# 数组方法



# 对象方法

# 类

# Promise

