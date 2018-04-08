# css
- css优先级：
    内联样式 > id选择器 > 类选择器 > 元素选择器

## Background
- background-color
```css
body {background-color:#b0c4de;}
```
- background-image
```css
body {background-image:url('paper.gif');}
```

- background-repeat(平铺)
```css
body
{
background-image:url('gradient2.png');
}（默认水平垂直都平铺）
```

```css
body
{
background-image:url('gradient2.png');
background-repeat:repeat-x;
}（只在水平方向平铺）
```

- background-attachment（背景是否随页面滚动）

 scroll（随页面滚动）
 
 fixed	（背景固定）
 
 inherit（从父元素继承）

- background-position （指定背景图片的位置）

```css
body
{
background-image:url('img_tree.png');
background-repeat:no-repeat;
background-position:right top;
}
```

## Text


- color	设置文本颜色
```css
body {color:red;}
```

- direction	设置文本方向。

ltr	默认。文本方向从左到右。

rtl	文本方向从右到左。

inherit	规定应该从父元素继承 direction 属性的值。

- letter-spacing	设置字符间距（允许负值）
```css
h1 {letter-spacing:2px;}
```

- line-height	设置行高

normal	默认。设置合理的行间距。

number	设置数字，此数字会与当前的字体尺寸相乘来设置行间距。

length	设置固定的行间距。

%	基于当前字体尺寸的百分比行间距。

inherit	规定应该从父元素继承 line-height 属性的值。

- text-align	对齐元素中的文本

left	把文本排列到左边。默认值：由浏览器决定。

right	把文本排列到右边。

center	把文本排列到中间。

justify	实现两端对齐文本效果。

inherit	规定应该从父元素继承 text-align 属性的值。

- text-decoration	向文本添加修饰

none	默认。定义标准的文本。

underline	定义文本下的一条线。

overline	定义文本上的一条线。

line-through	定义穿过文本下的一条线。

blink	定义闪烁的文本。

inherit	规定应该从父元素继承 text-decoration 属性的值。

- text-indent	缩进元素中文本的首行

length	定义固定的缩进。默认值：0。

%	定义基于父元素宽度的百分比的缩进。

inherit	规定应该从父元素继承 text-indent 属性的值。

- text-shadow	设置文本阴影
```css
h1
{
    text-shadow: 2px 2px 4px #ff0000;
}
```

h-shadow	必需。水平阴影的位置。允许负值。

v-shadow	必需。垂直阴影的位置。允许负值。

blur	可选。模糊的距离。

color	可选。阴影的颜色。参阅 CSS 颜色值。

- text-transform	控制元素中的字母

none	默认。定义带有小写字母和大写字母的标准的文本。

capitalize	文本中的每个单词以大写字母开头。

uppercase	定义仅有大写字母。

lowercase	定义无大写字母，仅有小写字母。

inherit	规定应该从父元素继承 text-transform 属性的值。

- vertical-align	设置元素的垂直对齐
- white-space	设置元素中空白的处理方式

pre	空白会被浏览器保留。其行为方式类似 HTML 中的  标签。

nowrap	文本不会换行，文本会在在同一行上继续，直到遇到 标签为止。

- word-spacing 设置字间距
```css
p
{ 
word-spacing:30px;
}
```

## Fonts

- font	在一个声明中设置所有的字体属性
- font-family	指定文本的字体系列
```css
p
{
font-family:"Times New Roman",Georgia,Serif;
}
```

- font-size	指定文本的字体大小

xx-small
x-small
small
medium
large
x-large
xx-large
把字体的尺寸设置为不同的尺寸，从 xx-small 到 xx-large。

默认值：medium。

smaller	把 font-size 设置为比父元素更小的尺寸。

larger	把 font-size 设置为比父元素更大的尺寸。

length	把 font-size 设置为一个固定的值。

%	把 font-size 设置为基于父元素的一个百分比值。

inherit	规定应该从父元素继承字体尺寸。

- font-style	指定文本的字体样式

normal	默认值。浏览器显示一个标准的字体样式。

italic	浏览器会显示一个斜体的字体样式。

oblique	浏览器会显示一个倾斜的字体样式。

inherit	规定应该从父元素继承字体样式。

- font-variant	以小型大写字体或者正常字体显示文本。
```css
p.small
{
font-variant:small-caps;
}(小型大写字母的字体。)
```

- font-weight	指定字体的粗细。

normal	默认值。定义标准的字符。

bold	定义粗体字符。

bolder	定义更粗的字符。

lighter	定义更细的字符。
100
200
300
400
500
600
700
800
900

定义由粗到细的字符。400 等同于 normal，而 700 等同于 bold。

inherit	规定应该从父元素继承字体的粗细。

## 链接（Link）

```css
a:link {color:#000000;}      /* 未访问链接*/
a:visited {color:#00FF00;}  /* 已访问链接 */
a:hover {color:#FF00FF;}  /* 鼠标移动到链接上 */
a:active {color:#0000FF;}  /* 鼠标点击时 */
```
a:link - 正常，未访问过的链接

a:visited - 用户已访问过的链接

a:hover - 当用户鼠标放在链接上时

a:active - 链接被点击的那一刻

> a:hover 必须跟在 a:link 和 a:visited后面

> a:active 必须跟在 a:hover后面

## 列表样式

```css
ul.a {list-style-type: circle;}
ul.b {list-style-type: square;}
 
ol.c {list-style-type: upper-roman;}
ol.d {list-style-type: lower-alpha;}
```

- list-style	简写属性。用于把所有用于列表的属性设置于一个声明中

- list-style-image	将图象设置为列表项标志。

- list-style-position	设置列表中列表项标志的位置。

inside	列表项目标记放置在文本以内，且环绕文本根据标记对齐。

outside	默认值。保持标记位于文本的左侧。列表项目标记放置在文本以外，且环绕文本不根据标记对齐。

- list-style-type	设置列表项标志的类型。

none	无标记。

disc	默认。标记是实心圆。

circle	标记是空心圆。

square	标记是实心方块。

decimal	标记是数字。

decimal-leading-zero	0开头的数字标记。(01, 02, 03, 等。)

lower-roman	小写罗马数字(i, ii, iii, iv, v, 等。)

upper-roman	大写罗马数字(I, II, III, IV, V, 等。)

lower-alpha	小写英文字母The marker is lower-alpha (a, b, c, d, e, 等。)

upper-alpha	大写英文字母The marker is upper-alpha (A, B, C, D, E, 等。)

lower-greek	小写希腊字母(alpha, beta, gamma, 等。)

lower-latin	小写拉丁字母(a, b, c, d, e, 等。)

upper-latin	大写拉丁字母(A, B, C, D, E, 等。)

hebrew	传统的希伯来编号方式

armenian	传统的亚美尼亚编号方式

georgian	传统的乔治亚编号方式(an, ban, gan, 等。)

cjk-ideographic	简单的表意数字

hiragana	标记是：a, i, u, e, o, ka, ki, 等。（日文片假名）

katakana	标记是：A, I, U, E, O, KA, KI, 等。（日文片假名）

hiragana-iroha	标记是：i, ro, ha, ni, ho, he, to, 等。（日文片假名）

katakana-iroha	标记是：I, RO, HA, NI, HO, HE, TO, 等。（日文片假名）

## Table
```css
table, th, td
{
border: 1px solid black;
}
```
表格边框，**注意会有两条边框**
```css
table
{
border-collapse:collapse;
}
table,th, td
{
border: 1px solid black;
}
```
border-collapse:collapse : 折叠边框
