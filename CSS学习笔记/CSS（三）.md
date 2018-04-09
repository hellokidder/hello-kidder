## CSS Float(浮动)

CSS 的 Float（浮动），会使元素向左或向右移动，其周围的元素也会重新排列。

元素的水平方向浮动，意味着元素只能左右移动而不能上下移动。

一个浮动元素会尽量向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。

浮动元素之后的元素将围绕它。

浮动元素之前的元素将不会受到影响。

---

clear	

指定不允许元素周围有浮动元素。

left
right
both
none
inherit	

---

float

指定一个盒子（元素）是否可以浮动。

left
right
none
inherit

## CSS 布局 - 水平 & 垂直对齐

- 元素居中对齐

要水平居中对齐一个元素(如 < div >), 可以使用 margin: auto;。

设置到元素的宽度将防止它溢出到容器的边缘。

元素通过指定宽度，并将两边的空外边距平均分配

```css
.center {
    margin: auto;
    width: 50%;
    border: 3px solid green;
    padding: 10px;
}
```

- 文本居中对齐

如果仅仅是为了文本在元素内居中对齐，可以使用 text-align: center;

```css
.center {
    text-align: center;
    border: 3px solid green;
}
```

- 要让图片居中对齐, 可以使用 margin: auto; 并将它放到 块 元素中:
```css
img {
    display: block;
    margin: auto;
    width: 40%;
}
```

- 左右对齐 - 使用定位方式

我们可以使用 position: absolute; 属性来对齐元素:

```css
.right {
    position: absolute;
    right: 0px;
    width: 300px;
    border: 3px solid #73AD21;
    padding: 10px;
}
```
**当使用 position 属性时，IE8以及更早的版本存在一个问题。如果容器元素设置了指定的宽度，并且省略了 !DOCTYPE 声明，那么 IE8 以及更早的版本会在右侧增加 17px 的外边距。**

- 左右对齐 - 使用 float 方式

我们也可以使用 float 属性来对齐元素:
```css
.right {
    float: right;
    width: 300px;
    border: 3px solid #73AD21;
    padding: 10px;
}
```
- 垂直居中对齐 - 使用 padding
- 
CSS 中有很多方式可以实现垂直居中对齐。 一个简单的方式就是头部顶部使用 padding:

```css
.center {
    padding: 70px 0;
    border: 3px solid green;
}
```

如果要水平和垂直都居中，可以使用 padding 和 text-align: center:

```css
.center {
    padding: 70px 0;
    border: 3px solid green;
    text-align: center;
}
```

垂直居中 - 使用 line-height

```css
.center {
    line-height: 200px;
    height: 200px;
    border: 3px solid green;
    text-align: center;
}
 
/* 如果文本有多行，添加以下代码: */
.center p {
    line-height: 1.5;
    display: inline-block;
    vertical-align: middle;
}
```

- 垂直居中 - 使用 position 和 transform

除了使用 padding 和 line-height 属性外,我们还可以使用 transform 属性来设置垂直居中:

```css
.center { 
    height: 200px;
    position: relative;
    border: 3px solid green; 
}
 
.center p {
    margin: 0;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

## CSS 组合选择符

- 在 CSS3 中包含了四种组合方式:

后代选取器(以空格分隔)

子元素选择器(以大于号分隔）

相邻兄弟选择器（以加号分隔）

普通兄弟选择器（以破折号分隔）

---

- 后代选取器

后代选取器匹配所有值得元素的后代元素。

```css
div p
{
  background-color:yellow;
}
```

- 子元素选择器

与后代选择器相比，子元素选择器（Childselectors）只能选择作为某元素子元素的元素。(直接子元素)

```css
div>p
{
  background-color:yellow;
}
```

- 相邻兄弟选择器

相邻兄弟选择器（Adjacentsiblingselector）可选择紧接在另一元素后的元素，且二者有相同父元素。

如果需要选择紧接在另一个元素后的元素，而且二者有相同的父元素，可以使用相邻兄弟选择器（Adjacent sibling selector）。

以下实例选取了所有位于 < div > 元素后的第一个 < p > 元素:

```css
div+p
{
  background-color:yellow;
}
```
- 后续兄弟选择器

后续兄弟选择器选取所有指定元素之后的相邻兄弟元素。

以下实例选取了所有 < div> 元素之后的所有相邻兄弟元素 < p> : 

```css
div~p
{
  background-color:yellow;
}
```

## CSS 下拉菜单

```
<style>
.dropdown {
    position: relative;
    display: inline-block;
}

.dropdown-content {
    display: none;
    position: absolute;
    background-color: #f9f9f9;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    padding: 12px 16px;
    z-index: 1;
}

.dropdown:hover .dropdown-content {
    display: block;
}
</style>

<div class="dropdown">
  <span>Mouse over me</span>
  <div class="dropdown-content">
    <p>Hello World!</p>
  </div>
</div>
```
第二个完整的实例
```
<style>
/* 下拉按钮样式 */
.dropbtn {
    background-color: #4CAF50;
    color: white;
    padding: 16px;
    font-size: 16px;
    border: none;
    cursor: pointer;
}

/* 容器 <div> - 需要定位下拉内容 */
.dropdown {
    position: relative;
    display: inline-block;
}

/* 下拉内容 (默认隐藏) */
.dropdown-content {
    display: none;
    position: absolute;
    background-color: #f9f9f9;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
}

/* 下拉菜单的链接 */
.dropdown-content a {
    color: black;
    padding: 12px 16px;
    text-decoration: none;
    display: block;
}

/* 鼠标移上去后修改下拉菜单链接颜色 */
.dropdown-content a:hover {background-color: #f1f1f1}

/* 在鼠标移上去后显示下拉菜单 */
.dropdown:hover .dropdown-content {
    display: block;
}

/* 当下拉内容显示后修改下拉按钮的背景颜色 */
.dropdown:hover .dropbtn {
    background-color: #3e8e41;
}
</style>

<div class="dropdown">
  <button class="dropbtn">下拉菜单</button>
  <div class="dropdown-content">
    <a href="#">菜鸟教程 1</a>
    <a href="#">菜鸟教程 2</a>
    <a href="#">菜鸟教程 3</a>
  </div>
</div>
```

## CSS 图像透明/不透明

```css
img
{
  opacity:0.4;
  filter:alpha(opacity=40); /* IE8 及其更早版本 */
}
```

## CSS 属性 选择器

- 属性选择器

下面的例子是把包含标题（title）的所有元素变为蓝色：
```css
[title]
{
    color:blue;
}
```
- 属性和值选择器

下面的实例改变了标题title='runoob'元素的边框样式:

```css
[title=runoob]
{
    border:5px solid green;
}
```

- 属性和值的选择器 - 多值

下面是包含指定值的title属性的元素样式的例子，使用（~）分隔属性和值:
```css
[title~=hello] { color:blue; }
```
下面是包含指定值的lang属性的元素样式的例子，使用（|）分隔属性和值:
```css
[lang|=en] { color:blue; }
```

- 表单样式

属性选择器样式无需使用class或id的形式:

```css
input[type="text"]
{
    width:150px;
    display:block;
    margin-bottom:10px;
    background-color:yellow;
}
input[type="button"]
{
    width:120px;
    margin-left:35px;
    display:block;
}
```