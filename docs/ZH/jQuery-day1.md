# jQuery

# 本篇笔记目标

- 能说出jQuery是什么
- 能够说出jQuery的优点
- 能说出JQuery对象和DOM对象的区别
- 能够使用jQuery常用API，如jQuery选择器、筛选选择器、jQuery筛选方法
- 理解并能够使用链式编程
- 理解并能运用排他思想

# 一、jQuery初识

## jQuery概念

​	jQuery是一个快速、简介的JavaScript库，是一个封装好的特定的方法和函数的集合。学习jQuery就是为了快速学习和调用这些函数和方法。其宗旨是“Write less, do more.” 即写更少的代码，做更多的事情。

> JavaScript库：
>
> jQuery, Prototype, YUI, Dojo, Ext JS, 移动端的zepto, 都是对原生JavaScript的封装，内部都是用JavaScript实现的。

## JQuery下载

​	官网地址：https://jquery.com/

## jQuery使用步骤

- 下载jQuery文件
- 引入jQuery 文件
- 使用

# 二、jQuery 入门

## 入口函数

​	第一种写法 **（推荐写法）**：

```js
$(function() {
    //此处是页面DOM加载完成的入口
})
```

​	第二种写法：

```js
$(document).ready(function() {
   //此处是页面DOM加载完成的入口 
});
```

​	注意点：

- 等着DOM结构渲染完毕即可执行内部代码，不必等到所有的外部资源加载完成，jQuery帮我们完成了封装
- 原生js中`widow.onload = function () {}`是等页面文档，外部js文件，css文件，图片加载完毕才执行内部代码。

## jQuery的基本使用

### jQuery的顶级对象 $

- $ === jQuery, 代码中可以相互代替，但为了方便。一般都直接用jQuery
- $ 是jQuery的顶级对象，相当于原生js中的window，把它包装成jQuery对象，就可以调用jQuery的方法。

### JQuery对象和DOM对象

- 区分jQuery对象和DOM对象获取元素和修改样式的方法
  - js对象只能用js的属性和方法
  - jQuery对象只能用jQuery的属性和方法

```js
//jQuery获取元素
$('选择器（元素）')
//原生js获取元素
document.querySelector('选择器（元素）')
document.getElementById('btn');

//jQuery修改样式
$('选择器（元素）').css('属性','值')
//原生js修改样式
btn.style.backgroundColor = "red"
```

- 理解jQuery对象本质：利用$对象包装后产生的对象，以伪数组的形式存储

- 相互转换

  原生js比jQuery更强大，原生的一些属性和方法在jQuery中没有封装，要想使用这些属性和方法就需要把jQuery对象转换为DOM对象才能使用

```js
//DOM对象转换为jQuery对象 $(DOM对象)
var btn = document.querySelector('input');
btn.style.background = 'red';
=====>>
$(btn).css('background','yellow');

//jQuery 对象转换为 DOM 对象（两种方式）
$('input')
=====>>
$('input')[0]
$('input').get(0)
```

# 三、常用API

### 目录：

- jQuery 选择器
- jQuery 样式操作
- jQuery 效果
- jQuery 属性操作
- jQuery 文本属性值
- jQuery 元素操作
- jQuery 尺寸、位置操作

### jQuery 选择器

```js
$('#id') // 指定id元素
$('*') // 所有元素
$('.class') // 指定class元素
$('div') // 根据标签获取元素
$('div,p,li') // 获取多个元素
$('li.class') // 交集获取
$('ul>li') // 获取子代
$('ul li') // 后代
```

#### 隐式迭代

遍历内部DOM元素（**伪数组的形式存储**）的过程就是隐式迭代。

```html
<ul>
	<li>1</li>
	<li>2</li>
	<li>3</li>
	<li>4</li>
</ul>
```

```js
//原生js
var lis = document.querySelectorAll('li');
for (var i = 0; i < lis.length; i++) {
lis[i].style.background = 'red';
}
//jQuery
$('li').css('background','red');//无需遍历循环，jquery内部已操作，$('li)返回的就是伪数组形式，无论有几个元素
```



#### jQuery筛选选择器

```js
$('li:first')// 第一个元素
$('li:last')// 最后一个元素
$('li:eq(2)')// **索引**为2的元素
$('li:odd')// **索引**为奇数的元素
$('li:even')// **索引**为偶数的元素
```

#### jQuery 筛选方法  **重点**

```js
$('li').parent()//父级
$('li').children()//子级--不添加参数，获取所有，有参数，按参数指定的找
$('li').find()//后代
$('li').siblings()//兄弟
$('li').nextAll()//后面的
$('li').prevAll()//前面的
```

判断是否有某个类名
```js
$('div').hasClass('aa') //返回布尔值
```

指定索引方法 `$('div').eq(index)`**推荐使用**

```js
$('li:eq(2)') //括号内必须是数字，给出值，不能是变量

$('div').eq(index) //index可以是变量，**推荐**使用
```

添加事件

```js
$('.btn1').click(function() {
    $('.box').show();
});
$('.btn2').click(function() {
    $('.box').hide();
});
```

小练习：

```html
<input type="button" value="点击1">
<input type="button" value="点击2">
<input type="button" value="点击3">
<input type="button" value="点击4">
<input type="button" value="点击5">
```

```js
//练习一：
//点击哪个按钮，就打印哪个按钮
$(input).click(function () {
   console.log($(this)); //伪数组形式
    console.log($(this)[0]);//元素
});
```

```js
//练习二：
//点谁让谁的背景颜色改变为红色，其他的不准改变
$('input').click(function () {
    $(this).css('background','red').siblings().css('background','');
});
```

```js
////练习三：
//点击哪个input把点击的这个input的索引值打印出来
$('input').click(function () {
    var index = $(this).index;
    console.log(index);//jQuery里直接就有index()方法，可直接使用
});
```

#### 排他思想

当前元素设置样式，其他兄弟元素清除样式。参考以上练习二。

#### 链式编程

```js
$(this).css('color', 'red').siblings().css('color', "");
```

### jQuery 样式操作

两种方法：直接修改css属性，或者操作类名

#### 直接操作css方法

```js
$(this).css('color');//参数只写属性名，则是返回属性值
$(this).css('color','red');//参数是属性名、属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可不加单位和引号
$(this).css({'color':white,
            'font-size':20});//参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开，属性如果是数字可以不加引号
```

#### 设置类样式

作用等同于原生js的classList，可以操作类里面的参数，注意参数不要加点

```js
$('div').addClass('current');//添加类
$('div').removeClass('current');//移除类
$('div').toggleClass('current');//切换类
```

**注意**：原生js里的className会覆盖元素原先的类名，jQuery里面类操作只是对指定类进行操作，不影响原先的类名

### jQuery 效果

#### 显示隐藏效果

```js
show([speed,[easing],[fn]])
hide([speed,[easing],[fn]])
toggle([speed,[easing],[fn]])


（1）参数都可以省略， 无动画直接显示。
（2）speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
（3）easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
（4）fn:  回调函数，在动画完成时执行的函数，每个元素执行一次。
```

#### 滑动效果

```js
slideDown([speed,[easing],[fn]])
slideUp([speed,[easing],[fn]])
slideToggle([speed,[easing],[fn]])


（1）参数都可以省略。
（2）speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
（3）easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
（4）fn:  回调函数，在动画完成时执行的函数，每个元素执行一次
```

#### 事件切换

```js
hover([over],out)

$('div').hover(function () {
    // 鼠标进入要做的事情
    $(this).css('background','blue');
},function () {
    // 鼠标离开要做的事情
    $(this).css('background','yellow');
});

（1）over:鼠标移到元素上要触发的函数（相当于mouseenter）
mouseenter==mouseover
（2）out:鼠标移出元素要触发的函数（相当于mouseleave）
mouseleave==mouseout
（3）如果只写一个函数，则鼠标经过和离开都会触发它
```

小知识：`onmouseover`和`onmouseenter`效果看起来是差不多的。但有以下不同：

  - `onmouseover`：支持事件冒泡，`onmouseenter`：不支持事件冒泡。所以在使用的过程中，因为mouseover支持冒泡，所以在父级元素内移动是，可能会多次触发事件，建议大家谨慎使用`mouseover`。
  - `onmouseenter`比`onmouseover`效率更高。以下是代码例子：

```html
<button id="btn"></button>
```

```js
var btn = document.getElementById('btn');
btn.onmouseover = function () {
      alert(4);
      console.log('over');
}
btn.onmouseenter = function () {
      alert(3);
      console.log('enter')
}
    
```

​    输出结果是：

> over
>
> [Violation] 'mouseover' handler took 1001ms
>
> enter
>
> [Violation] 'mouseenter' handler took 195ms

看不到毫秒数，记得到console下找到All levels，勾选上verbose就OK啦！

#### 动画队列及其停止排队方法

```js
//动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行
stop()//停止排队
(1）stop() 方法用于停止动画或效果。
(2)  注意： stop() 写到动画或者效果的前面， 相当于停止结束上一次的动画
```

#### 淡入淡出效果

```js
fadeIn([speed,[easing],[fn]])
fadeOut([speed,[easing],[fn]])
fadeToggle([speed,[easing],[fn]])
fadeTo([[speed],opacity,[easing],[fn]])【注意fadeTo必须写两个参数，speed和opacity】


（1）参数都可以省略。
（2）speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
（3）easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
（4）fn:  回调函数，在动画完成时执行的函数，每个元素执行一次。
```

#### 自定义动画

```js
语法：animate(params,[speed],[easing],[fn])

参数：
（1）params: 想要更改的样式属性，以对象形式传递，必须写。 属性名可以不用带引号， 如果是复合属性则需要采取驼峰命名法 borderLeft。其余参数都可以省略。
（2）speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
（3）easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
（4）fn:  回调函数，在动画完成时执行的函数，每个元素执行一次。
```

