## DOM

### 01-节点的创建、修改、添加  <!-- {docsify-ignore} -->

- 创建

  - `innerHTML`

  ```js
  //元素.innerHTML = 'html标签结构'
  ul.innerHTML = '<li>狗蛋</li>';
  ```

  - `document.write()`;

  ```js
  //会把页面已经存在的HTML结构覆盖掉
  //该方法可以解析HTML结构，多次写，多次输出
  document.write('<div>新的标签</div>');
  ```

  - `document.creatElement()`

  ```js
  //document.createElement('li');
  document.creatElement('标签名');
  ```

- 添加

  - a`ppendChild()`

    ```js
    //appendChild 给一个父元素从后面追加一个子元素
    
    //创建新标签
    var li = document.creatElement('li');
    //给新标签添加内容
    li.innerText = '我是一个li';
    //把新创建的标签追加给ul
    ul.appendChild(li);
    ```

    

  - `insertBefore()`

    ```js
    //在某个子元素前面插入新的子元素
    
    //获取类名为second的元素对象
    var second = document.querySelector('.second');
    //创建一个新的元素对象li
    var li = document.creatElement('li');
    //给新元素对象添加内容
    li.innerText = '我是新的li';
    //在类名为second的元素对象前面添加一个新的元素对象li
    ul.insertBefore(li, second);
    ```

- 修改

  - `innerHTML`：修改结构
  - `innerText`：修改内容

  

### 02-通过节点获取节点 <!-- {docsify-ignore} -->



- 获取子元素（伪数组）

```js
//父元素.children
//可以得到某个父元素下的所有的子元素的集合，一个伪数组

//获取ul的DOM节点
var ul = document.querySelector('ul');
//打印ul下的所有子元素
console.log(ul.children);//HTMLCollection(5) [li, li, li, li, li]
```

- 获取父元素（一个）

```js
//元素.parentNode

//获取ul下第二个li元素
var li = document.querySelector('ul li:nth-child(2)');
//打印li的父元素节点
console.log(li.parentNode);//<ul>...</ul>
```



- 获取兄弟元素（一个）

```js
//返回上一个兄弟元素
console.log(li.previousElementSibling);
//返回上一个兄弟元素
console.log(li.nextElementSibling);
```

### 03-删除节点 <!-- {docsify-ignore} -->

```js
//父元素.removeChild(要删除的子元素)
var first = ul.children[0];
ul.removeChild(first);
```





## BOM

> `BOM`的核心对象是 `window`，它表示浏览器的一个实例。

### window对象 <!-- {docsify-ignore} -->

- 特点

  - 所有`window`对象的属性和方法，都可以直接省略`window`直接使用，因为`window`对象在浏览器中被称为**顶级对象**

  ```js
  document.getElementById('logo');
  console.log(window.document == document); //true
  ```

  

  - **顶级对象**：页面中所有的东西都是依赖于这个对象存在的

  - 变量与函数：
    - 所有的全局变量和全局函数都是`window`对象的属性和方法
    - 在`js`代码里，不使用`var`声明的变量，都是隐式全局变量，但这个方式是不推荐的，因为不使用`var`声明，不会变量提升。

  ```js
  // 全局变量和函数 都是window上的挂载
  var a = 10;
  console.log(window.a);
  
  function fn() {
      console.log(1);
  }
  window.fn();
  
  // 隐式变量：定义变量，变量赋值；
  b = 2;
  console.log(window.b);
  
  // 访问变量：无赋值，就是访问变量；报错，无定义；
  c;
  console.log(window.c);
  ```

- 方法：`onload`

  - 作用：页面所需的**静态资源**全部加载完毕的时候执行
  - 这个方法调用一般是用`window.onload `不省略`window`

  ```js
  window.onload = function() {
      //静态资源全部加载完成后，才执行这个函数
  }
  ```

- 方法：定时器

  - `setTimeout `一次性定时器
  - `clearTimeout`清除一次性定时器

  ```js
  //延迟一定的毫秒之后，调用函数一次
  //返回值：是该定时器的id，id可用于停止这个定时器
  var timer = setTimeout(function(){},延迟的毫秒数);
  var timer = setTimeout(function(){
      alert(1)
  },3000);
  
  //停止一次性的定时器，清除后，就不会执行这个定时器
  var btn = document.querySelector('#stop');
  btn.onclick = function() {
      clearTimeout(timer);
  };
  
  ```

  

  - `setInterval` 永久性定时器
  - `clearInterval` 清除永久性定时器

  ```js
  //setInterval
  //作用：阶段性地执行函数
  //返回值：该定时器的id
  var timer = setInterval(function(){},间隔时间);
  var timer = setInterval(function(){
      console.log(1);
  },1000);
  
  //清除永久定时器
  var btn = document.querySelector('#btn');
  btn.onclick = function() {
      clearInterval(timer);
  }
  
  ```

  **执行定时器，都是等待自己的间隔才开始执行**

- 属性：`location`

  - `location`: 负责管理浏览器地址栏相关的行为和信息的对象
  - 属性：` location.href` 该属性就是浏览器地址栏里面的内容
    - 获取当前浏览器的地址
    - 重新设置，页面就会发生跳转

  ```js
  //如果想要用js进行跳转，只需要location.href = 新的地址;
  location.href = "http://jd.com";
  ```

  

### `localStorage`和`JSON` <!-- {docsify-ignore} -->

`localStorage`

- 把操作的数据进行本地储存，刷新了数据还在，原来操作的没变
- 本地储存：本地指浏览器，储存指浏览器可以储存数据

```js
// 存储： 后面的值 前面可以放入任何数据类型，保存后为字符串；
// 注意： 如果存储的是对象之类的复杂类型，需要先把复杂类型转换为的字符串，再存进去；
// 多次对一个键进行赋值，会把前面的值覆盖；
localStorage.setItem(键, 值);
localStorage.setItem("name", "张三");
localStorage.setItem("age", 12);
localStorage.setItem("zhiye", "前端工程师");

//读取数据
//返回：我们存入的是数据的值，返回的是字符串
var a = localStorage.getItem("name");
console.log(a);

//没有值的话，返回null
var b = localStorage.getItem('age');
console.log(b);

// 删除键的值
localStorage.removeItem(键);　
localStorage.removeItem("name");


// 全部清空
localStorage.clear();　
```

`JSON`

`JSON`格式：**[] - 表示数组；{} - 对象；和JS学习的对象，数组特别的像；**

- JSON是**有一定格式的字符串**
  - 所有的键必须使用双引号包起来
  - 字符串也必须是双引号
  - 只有数字和字符串两种类型
  - 只是记录数据；

- `JSON`方法：我们自己转json格式比较麻烦；js提供了JSON方法，里面封装好了很多跟json操作相关的方法

```js
//将对象转换为json格式的字符串
//返回值：一个满足json格式的字符串
JSON.stringgify(对象);

//讲json格式的字符串转换为对象
//返回值：依赖于你的json格式字符串，可能返回数组，或者是对象。。。
JSON.parse(json格式字符串);
```

- `JSON`:
  - 字符串，约定的数据格式的字符串
  - BOM的一个方法：将对象类型转为JSON字符串