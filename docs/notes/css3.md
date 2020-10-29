## css水平、垂直居中

* 水平居中
  1. 行内元素：`text-align:center`
  2. 块级元素：`margin: 0 auto`
  3. `position: absolute; left: 50%; transform: translateX(-50%)`
  4.  `display: flex; jusitify-content: center;`
* 垂直居中
  1. `height: 50px; line-height: 50px;`
  2. `position: absolute; top: 50%; transform: translateY(-50%)`
  3. `display: flex; align-items: center;`
  4. `.table{display: table;} .cell {display:table-cell;vertical-align: middle;}`
  ```html
      <!-- 垂直居中第四种html代码 -->
    <div class="table">
      <div class="cell">这是中间的文字</div>
    </div>
  ```
  ```css
  /* 垂直居中第四种css代码 */
    .table {display: table;width: 150px;height:150px; background: #ccc;}
    .cell {display:table-cell;vertical-align: middle;}
  ```

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"></meta>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"></meta>
  <title>Document</title>
  <style>
    .table {display: table;width: 150px;height:150px; background: #ccc;}
    .cell {display:table-cell;vertical-align: middle;}
  </style>
  <body>
    <div class="table">
      <div class="cell">垂直居中第四种效果</div>
    </div>
  </body>
  </html>

## px、em、rem、vh

>px

px像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。

> em

em是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。

> rem

相对单位。但相对的只是HTML根元素。

> vw/vh

Viewport Width 和 Viewport Height。视窗的宽度和高度，1vw 和 1vh相当于屏幕宽度和高度的1%。

## 画一条0.5px的直线

```css
height: 1px;
transform: scale(0.5)
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"></meta>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"></meta>
  <title>Document</title>
  <style>
  .half {height:1px;background:red;transform: scale(1, 0.5)}
  .normal {height:1px;background:red;}
  </style>
  <body>
    <div>这是0.5px的红线</div>
    <br>
    <div class="half"></div>
    <br>
    <div>这是1px的红线</div>
    <br>
    <div class="normal"></div>
  </body>
  </html>

## 盒模型

盒模型的组成，由里向外`content`,`padding`,`border`,`margin`.

> W3C标准盒子模型

`box-sizing: content-box`. `width`指`content`部分的宽度

> IE盒子模型

`box-sizing: border-box`. `width`表示`content`+`padding`+`border`这三个部分的宽度

## 画一个三角形

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"></meta>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"></meta>
  <title>Document</title>
  <style>
    .triangle {width: 0;height: 0;border-width:100px;border-style:solid;border-color: transparent transparent red transparent;}
  </style>
  <body>
    <div class="triangle"></div>
  </body>
  </html>

```css
    .triangle {
      width: 0;
      height: 0;
      border-width:100px;
      border-style:solid;
      border-color: transparent transparent red transparent;
    }
```

```html
<div class="triangle"></div>
```
## 清除浮动的方式及其原理

 清除浮动主要是为了解决，父元素因为子级元素浮动引起的内部高度为0的问题

> 额外标签法

```css
    .clear{
        clear:both;
    }
```

```html

    <div>
        <div class="floatbox">1</div>
        <div class="floatbox">2</div>
        <div class="clear"></div>
    </div>

```

> 父级添加overflow属性

```html
    <div style="overflow:hidden">
        <div class="floatbox">1</div>
        <div class="floatbox">2</div>
    </div>

```

> 使用after伪元素清除浮动

```css
.clearfix:after { /*伪元素是行内元素 正常浏览器清除浮动方法*/
  content: '';
  display: block;
  clear: both;
  height: 0;
  visibility: hidden;
}
.clearfix { /*ie6清除浮动的方式 *号只有IE6-IE7执行，其他浏览器不执行 */
 /* 触发 hasLayout  */
  *zoom: 1;
}
```

```html
    <div class="clearfix">
        <div class="floatbox">1</div>
        <div class="floatbox">2</div>
    </div>

```
> 使用before和after双伪元素清除浮动

```css
.clearfix:after,.clearfix:before{
  content: "";
  display: table;
}
.clearfix:after{
  clear: both;
}
.clearfix{
  *zoom: 1;
}
```
```html
    <div class="clearfix">
        <div class="floatbox">1</div>
        <div class="floatbox">2</div>
    </div>

```
