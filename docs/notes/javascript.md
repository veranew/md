## Number类型转String类型

> String()

> toString()

> toExponential()

一个用幂的形式 (科学记数法) 来表示[`Number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number) 对象的字符串。

```js
// 对数值字面量使用 toExponential() 方法，且该数值没有小数点和指数时，应该在该数值与该方法之间隔开一个空格，以避免点号被解释为一个小数点。也可以使用两个点号调用该方法。
77.1234.toExponential()   //输出 7.71234e+1
77 .toExponential()   //输出 7.7e+1
```



> toFixed()

使用定点表示法表示给定数字的字符串。

```js
-2.34.toFixed(1);         // 返回 -2.3 （由于操作符优先级，负数不会返回字符串）
(-2.34).toFixed(1);       // 返回 "-2.3" （若用括号提高优先级，则返回字符串）
```

> toPrecision()

以定点表示法或指数表示法表示的一个数值对象的字符串表示，四舍五入到 `precision` 参数指定的显示数字位数。

```js
var numObj = 5.123456;
numObj.toPrecision(1) // 输出 5
numObj.toPrecision(5) // 输出 5.1235
// 注意：在某些情况下会以指数表示法返回
console.log((1234.5).toPrecision(2)); // "1.2e+3"
```

## 运算符

常见运算符如加法 `+` 、减法 `-` 、乘法 `*` 和除法 `/` ，举一个例子，来介绍一些概念：

```js
let sum = 1 + 2;
let age = +18;
```

其中：

- 加法运算 `1 + 2` 中， `1` 和 `2` 为 2 个运算元，左运算元 `1` 和右运算元 `2` ，即**「运算元就是运算符作用的对象。」**
- `1 + 2` 运算式中包含 2 个运算元，因此也称该运算式中的加号  `+` 为 **「二元运算符。」**
- 在 `+18` 中的加号 `+` 对应只有一个运算元，则它是 **「一元运算符」** 。

## 值的比较

>  **相等性判断（Object.is()）**

```js
Object.is(value1, value2);
```

以下任意项成立则两个值相同：
1. 两个值都是 undefined
2. 两个值都是 null
3. 两个值都是 true 或者都是 false
4. 两个值是由相同个数的字符按照相同的顺序组成的字符串
5. 两个值指向同一个对象
6. 两个值都是数字并且
  	1. 都是正零 +0
  	2. 都是负零 -0
  	3. 都是 NaN
  	4. 都是除零和 NaN 外的其它同一个数字
 

使用示例：


```js
Object.is('foo', 'foo');     // true
Object.is(window, window);   // true
Object.is('foo', 'bar');     // false
Object.is([], []);           // false
var foo = { a: 1 };
var bar = { a: 1 };
Object.is(foo, foo);         // true
Object.is(foo, bar);         // false
Object.is(null, null);       // true
// 特例
Object.is(0, -0);            // false
Object.is(0, +0);            // true
Object.is(-0, -0);           // true
Object.is(NaN, 0/0);         // true
```

兼容性 Polyfill 处理：

```
if (!Object.is) {
  Object.is = function(x, y) {
    // SameValue algorithm
    if (x === y) { // Steps 1-5, 7-10
      // Steps 6.b-6.e: +0 != -0
      return x !== 0 || 1 / x === 1 / y;
    } else {
      // Step 6.a: NaN == NaN
      return x !== x && y !== y;
    }
  };
}
```

>  **null 与 undefined 比较**

1. 对于相等性判断比较简单：

```js
null == undefined;  // true
null === undefined; // false
```

2. 对于其他比较，它们会先转换位数字：`null` 转换为 `0` ， `undefied` 转换为 `NaN` 。

`undefined` 和 `null` 在相等性检查 `==` 中**「不会进行任何的类型转换」**，它们有自己独立的比较规则，所以除了它们之间互等外，不会等于任何其他的值。

```js
null > 0;  // false 1  *******
null >= 0; // true  2  *********
null == 0; // false 3  ********
null < 1;  // true  4  **********
```

```js
undefined > 0;  // false  1
undefined > 1;  // false  2
undefined == 0; // false  3
```

## 函数表达式 和 函数声明 的区别

> 语法差异

```js
// 函数表达式
let fun = function(){};
// 函数声明
function fun(){}
```

> 创建时机差异

函数表达式会在代码执行到达时被创建，并且仅从那一刻可用。

而函数声明被定义之前，它就可以被调用。

```js
// 函数表达式
fun();  // Uncaught ReferenceError: fun is not defined
let fun = function(){console.log('leo')};
// 函数声明
fun();  // "leo"
function fun(){console.log('leo')};
```

> 使用建议

建议优先考虑函数声明语法，它能够为组织代码提供更多灵活性，因为我们可以在声明函数前调用该函数。

## 箭头函数

1. 箭头函数不存在`this`；
2. 箭头函数不能当做**「构造函数」**，即不能用`new`实例化；
3. 箭头函数不存在`arguments`对象，即不能使用，可以使用`rest`参数代替；
4. 箭头函数不能使用`yield`命令，即不能用作Generator函数。

