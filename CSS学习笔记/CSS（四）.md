左上角，第二个值为右上角，第三个值为右下角，第四个值为左下角。

三个值: 第一个值为左上角, 第二个值为右上角和左下角，第三个值为右下角

两个值: 第一个值为左上角与右下角，第二个值为右上角与左下角

一个值： 四个圆角值相同
- CSS3 盒阴影

CSS3 中的 box-shadow 属性被用来添加阴影:

```css
div
{
box-shadow: 10px 10px 5px #888888;
}
```
- CSS3 边界图片

有了 CSS3 的 border-image 属性，你可以使用图像创建一个边框：
```css
div
{
border-image:url(border.png) 30 30 round;
-webkit-border-image:url(border.png) 30 30 round; /* Safari 5 and older */
-o-border-image:url(border.png) 30 30 round; /* Opera */
}
```
border-image-source	用于指定要用于绘制边框的图像的位置

border-image-slice	图像边界向内偏移

border-image-width	图像边界的宽度

border-image-outset	用于指定在边框外部绘制 border-image-area 的量

border-image-repeat	用于设置图像边界是否应重复（repeat）、拉伸（stretch）或铺满（round）。

## CSS3 背景

- CSS3 background-image属性

不同的背景图像和图像用逗号隔开，所有的图片中显示在最顶端的为第一张。
```css
#example1 { 
    background-image: url(img_flwr.gif), url(paper.gif); 
    background-position: right bottom, left top; 
    background-repeat: no-repeat, repeat; 
}
```
```css
#example1 {
    background: url(img_flwr.gif) right bottom no-repeat, url(paper.gif) left top repeat;
}
```
- CSS3 background-size 属性

CSS3中可以指定背景图片，让我们重新在不同的环境中指定背景图片的大小。您可以指定像素或百分比大小。

你指定的大小是相对于父元素的宽度和高度的百分比的大小。
```css
div
{
    background:url(img_flwr.gif);
    background-size:100% 100%;
    background-repeat:no-repeat;
}
```
- CSS3的background-Origin属性

background-Origin属性指定了背景图像的位置区域。

content-box, padding-box,和 border-box区域内可以放置背景图像。

![image](http://www.runoob.com/images/background-origin.gif)

```css
div
{
    background:url(img_flwr.gif);
    background-repeat:no-repeat;
    background-size:100% 100%;
    background-origin:content-box;
}
```

- CSS3 background-clip属性

CSS3中background-clip背景剪裁属性是从指定位置开始绘制。

```css
#example1 { 
    border: 10px dotted black; 
    padding: 35px; 
    background: yellow; 
    background-clip: content-box; 
}
```

## CSS3 渐变（Gradients）

CSS3 定义了两种类型的渐变（gradients）：

线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向

径向渐变（Radial Gradients）- 由它们的中心定义

---

- CSS3 线性渐变

为了创建一个线性渐变，你必须至少定义两种颜色结点。颜色结点即你想要呈现平稳过渡的颜色。同时，你也可以设置一个起点和一个方向（或一个角度）。


background: linear-gradient(direction, color-stop1, color-stop2, ...);

下面的实例演示了从顶部开始的线性渐变。起点是红色，慢慢过渡到蓝色：
```css
#grad {
  background: -webkit-linear-gradient(red, blue); /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(red, blue); /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(red, blue); /* Firefox 3.6 - 15 */
  background: linear-gradient(red, blue); /* 标准的语法 */
}
```

线性渐变 - 从左到右

下面的实例演示了从左边开始的线性渐变。起点是红色，慢慢过渡到蓝色：

```css
#grad {
  background: -webkit-linear-gradient(left, red , blue); /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(right, red, blue); /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(right, red, blue); /* Firefox 3.6 - 15 */
  background: linear-gradient(to right, red , blue); /* 标准的语法 */
}
```

线性渐变 - 对角

你可以通过指定水平和垂直的起始位置来制作一个对角渐变。

下面的实例演示了从左上角开始（到右下角）的线性渐变。起点是红色，慢慢过渡到蓝色：

```css
#grad {
  background: -webkit-linear-gradient(left top, red , blue); /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(bottom right, red, blue); /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(bottom right, red, blue); /* Firefox 3.6 - 15 */
  background: linear-gradient(to bottom right, red , blue); /* 标准的语法 */
}
```

使用角度

如果你想要在渐变的方向上做更多的控制，你可以定义一个角度，而不用预定义方向（to bottom、to top、to right、to left、to bottom right，等等）。

background: linear-gradient(angle, color-stop1, color-stop2);

角度是指水平线和渐变线之间的角度，逆时针方向计算。换句话说，0deg将创建一个从下到上的渐变，90deg 将创建一个从左到右的渐变。

![image](http://www.runoob.com/wp-content/uploads/2014/07/7B0CC41A-86DC-4E1B-8A69-A410E6764B91.jpg)

**但是，请注意很多浏览器(Chrome,Safari,fiefox等)的使用了旧的标准，即 0deg 将创建一个从左到右的渐变，90deg 将创建一个从下到上的渐变。换算公式 90 - x = y 其中 x 为标准角度，y为非标准角度。**

```css
#grad {
  background: -webkit-linear-gradient(180deg, red, blue); /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(180deg, red, blue); /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(180deg, red, blue); /* Firefox 3.6 - 15 */
  background: linear-gradient(180deg, red, blue); /* 标准的语法 */
}
```

使用多个颜色结点

下面的实例演示了如何设置多个颜色结点：

```css
#grad {
  background: -webkit-linear-gradient(red, green, blue); /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(red, green, blue); /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(red, green, blue); /* Firefox 3.6 - 15 */
  background: linear-gradient(red, green, blue); /* 标准的语法 */
}
```

使用透明度（transparent）

CSS3 渐变也支持透明度（transparent），可用于创建减弱变淡的效果。

```css
#grad {
  background: -webkit-linear-gradient(left,rgba(255,0,0,0),rgba(255,0,0,1)); /* Safari 5.1 - 6 */
  background: -o-linear-gradient(right,rgba(255,0,0,0),rgba(255,0,0,1)); /* Opera 11.1 - 12*/
  background: -moz-linear-gradient(right,rgba(255,0,0,0),rgba(255,0,0,1)); /* Firefox 3.6 - 15*/
  background: linear-gradient(to right, rgba(255,0,0,0), rgba(255,0,0,1)); /* 标准的语法 */
}
```
重复的线性渐变

repeating-linear-gradient() 函数用于重复线性渐变：

```css
#grad {
  /* Safari 5.1 - 6.0 */
  background: -webkit-repeating-linear-gradient(red, yellow 10%, green 20%);
  /* Opera 11.1 - 12.0 */
  background: -o-repeating-linear-gradient(red, yellow 10%, green 20%);
  /* Firefox 3.6 - 15 */
  background: -moz-repeating-linear-gradient(red, yellow 10%, green 20%);
  /* 标准的语法 */
  background: repeating-linear-gradient(red, yellow 10%, green 20%);
}
```

- CSS3 径向渐变

径向渐变由它的中心定义。

为了创建一个径向渐变，你也必须至少定义两种颜色结点。颜色结点即你想要呈现平稳过渡的颜色。同时，你也可以指定渐变的中心、形状（圆形或椭圆形）、大小。默认情况下，渐变的中心是 center（表示在中心点），渐变的形状是ellipse（表示椭圆形），渐变的大小是 farthest-corner（表示到最远的角落）。

background: radial-gradient(center, shape size, start-color, ...,last-color);

径向渐变 - 颜色结点均匀分布（默认情况下）
```css
#grad {
  background: -webkit-radial-gradient(red, green, blue); /* Safari 5.1 - 6.0 */
  background: -o-radial-gradient(red, green, blue); /* Opera 11.6 - 12.0 */
  background: -moz-radial-gradient(red, green, blue); /* Firefox 3.6 - 15 */
  background: radial-gradient(red, green, blue); /* 标准的语法 */
}
```
径向渐变 - 颜色结点不均匀分布
```css
#grad {
  background: -webkit-radial-gradient(red 5%, green 15%, blue 60%); /* Safari 5.1 - 6.0 */
  background: -o-radial-gradient(red 5%, green 15%, blue 60%); /* Opera 11.6 - 12.0 */
  background: -moz-radial-gradient(red 5%, green 15%, blue 60%); /* Firefox 3.6 - 15 */
  background: radial-gradient(red 5%, green 15%, blue 60%); /* 标准的语法 */
}
```
设置形状

shape 参数定义了形状。它可以是值 circle 或 ellipse。其中，circle 表示圆形，ellipse 表示椭圆形。默认值是 ellipse。

```css
#grad {
  background: -webkit-radial-gradient(circle, red, yellow, green); /* Safari 5.1 - 6.0 */
  background: -o-radial-gradient(circle, red, yellow, green); /* Opera 11.6 - 12.0 */
  background: -moz-radial-gradient(circle, red, yellow, green); /* Firefox 3.6 - 15 */
  background: radial-gradient(circle, red, yellow, green); /* 标准的语法 */
}
```

重复的径向渐变

repeating-radial-gradient() 函数用于重复径向渐变：

```css
#grad {
  /* Safari 5.1 - 6.0 */
  background: -webkit-repeating-radial-gradient(red, yellow 10%, green 15%);
  /* Opera 11.6 - 12.0 */
  background: -o-repeating-radial-gradient(red, yellow 10%, green 15%);
  /* Firefox 3.6 - 15 */
  background: -moz-repeating-radial-gradient(red, yellow 10%, green 15%);
  /* 标准的语法 */
  background: repeating-radial-gradient(red, yellow 10%, green 15%);
}
```

