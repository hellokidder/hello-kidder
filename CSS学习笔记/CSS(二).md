## 盒模型

![image](http://www.runoob.com/images/box-model.gif)

Margin(外边距) - 清除边框外的区域，外边距是透明的。

Border(边框) - 围绕在内边距和内容外的边框。

Padding(内边距) - 清除内容周围的区域，内边距是透明的。

Content(内容) - 盒子的内容，显示文本和图像。

**重要: 当指定一个CSS元素的宽度和高度属性时，你只是设置内容区域的宽度和高度。要知道，完全大小的元素，你还必须添加填充，边框和边距。**

> 最终元素的总宽度计算公式是这样的：

> 总元素的宽度=宽度+左填充+右填充+左边框+右边框+左边距+右边距

> 元素的总高度最终计算公式是这样的：

> 总元素的高度=高度+顶部填充+底部填充+上边框+下边框+上边距+下边距

## CSS 边框Border

- border	简写属性，用于把针对四个边的属性设置在一个声明。

- border-style	用于设置元素所有边框的样式，或者单独地为各边设置边框样式。

none: 默认无边框


dotted: 定义一个点线边框


dashed: 定义一个虚线边框


solid: 定义实线边框


double: 定义两个边框。 两个边框的宽度和 border-width 的值相同


groove: 定义3D沟槽边框。效果取决于边框的颜色值


ridge: 定义3D脊边框。效果取决于边框的颜色值


inset:定义一个3D的嵌入边框。效果取决于边框的颜色值


outset: 定义一个3D突出边框。 效果取决于边框的颜色值

- border-width	简写属性，用于为元素的所有边框设置宽度，或者单独地为各边边框设置宽度。

- border-color	简写属性，设置元素的所有边框中可见部分的颜色，或为 4 个边分别设置颜色。

## CSS 轮廓（outline)

![image](http://www.runoob.com/images/box_outline.gif)

outline	

在一个声明中设置所有的轮廓属性	

outline-color
outline-style
outline-width
inherit	

---

outline-color	

设置轮廓的颜色	

color-name
hex-number
rgb-number
invert
inherit	

---

outline-style	

设置轮廓的样式	

none
dotted
dashed
solid
double
groove
ridge
inset
outset
inherit	

---

outline-width	

设置轮廓的宽度	

thin
medium
thick
length
inherit

## CSS margin(外边距) padding（填充）

> margin 清除周围的（外边框）元素区域。margin 没有背景颜色，是完全透明的。

> margin 可以单独改变元素的上，下，左，右边距，也可以一次改变所有的属性。

![image](http://www.runoob.com/wp-content/uploads/2013/08/VlwVi.png)

auto	设置浏览器边距。这样做的结果会依赖于浏览器

length	定义一个固定的margin（使用像素，pt，em等）

%	定义一个使用百分比的边距

---

> 当元素的 padding（填充）内边距被清除时，所释放的区域将会受到元素背景颜色的填充。

> 单独使用 padding 属性可以改变上下左右的填充。

length	定义一个固定的填充(像素, pt, em,等)

%	使用百分比值定义一个填充

## 分组选择器

> 每个选择器用逗号分隔.

```css
h1,h2,p
{
color:green;
}
```

## 嵌套选择器

> 在下面的例子设置了三个样式：

> 为所有p元素指定一个样式

> 为所有class="marked"的元素指定一个样式

> 为所有class="marked"元素内的p元素指定一个样式

```css
p
{
color:blue;
text-align:center;
}
.marked
{
background-color:red;
}
.marked p
{
color:white;
}
```
## CSS 尺寸 (Dimension)

height	设置元素的高度。

line-height	设置行高。

max-height	设置元素的最大高度。

max-width	设置元素的最大宽度。

min-height	设置元素的最小高度。

min-width	设置元素的最小宽度。

width	设置元素的宽度。

## Display

-  Display(显示) 与 Visibility（可见性）

visibility:hidden可以隐藏某个元素，但隐藏的元素仍需占用与未隐藏之前一样的空间。也就是说，该元素虽然被隐藏了，但仍然会影响布局。

```css
h1.hidden {visibility:hidden;}
```
display:none可以隐藏某个元素，且隐藏的元素不会占用任何空间。也就是说，该元素不但被隐藏了，而且该元素原本占用的空间也会从页面布局中消失。
```css
h1.hidden {display:none;}
```

-  Display - 块和内联元素

display:block  -- 显示为块级元素

display:inline  -- 显示为内联元素

display:inline-block--显示为内联块元素，表现为同行显示并可修改宽高内外边距等属性  


块元素是一个元素，占用了全部宽度，在前后都是换行符。

内联元素只需要必要的宽度，不强制换行。

## CSS Positioning(定位)

position 属性的四个值：

static
relative
fixed
absolute

元素可以使用的顶部，底部，左侧和右侧属性定位。然而，这些属性无法工作，除非是先设定position属性。他们也有不同的工作方式，这取决于定位方法。

- static 定位

HTML元素的默认值，即没有定位，元素出现在正常的流中。

静态定位的元素不会受到 top, bottom, left, right影响。

- fixed 定位

元素的位置相对于浏览器窗口是固定位置。

即使窗口是滚动的它也不会移动：

```css
p.pos_fixed
{
    position:fixed;
    top:30px;
    right:5px;
}
```

**Fixed定位使元素的位置与文档流无关，因此不占据空间。**

**Fixed定位的元素和其他元素重叠。**

- relative 定位

相对定位元素的定位是相对其正常位置。

```css
h2.pos_left
{
    position:relative;
    left:-20px;
}
h2.pos_right
{
    position:relative;
    left:20px;
}
```
**可以移动的相对定位元素的内容和相互重叠的元素，它原本所占的空间不会改变。**

- absolute 定位

绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于 < html >

```css
h2
{
    position:absolute;
    left:100px;
    top:150px;
}
```

**absolute 定位使元素的位置与文档流无关，因此不占据空间。**

**absolute 定位的元素和其他元素重叠。**

---

clip	

剪辑一个绝对定位的元素	

shape
auto
inherit	2

---

**cursor**

显示光标移动到指定的类型

url
auto
crosshair
default
pointer
move
e-resize
ne-resize
nw-resize
n-resize
se-resize
sw-resize
s-resize
w-resize
text
wait
help	2

---

**overflow**

设置当元素的内容溢出其区域时发生的事情。

auto
hidden
scroll
visible
inherit	2

---
overflow-y

指定如何处理顶部/底部边缘的内容溢出元素的内容区域

auto
hidden
scroll
visible
no-display
no-content	2

---


overflow-x

指定如何处理右边/左边边缘的内容溢出元素的内容区域

auto
hidden
scroll
visible
no-display
no-content	2

---

**position**	

指定元素的定位类型

absolute
fixed
relative
static
inherit	2

---

**z-index**

设置元素的堆叠顺序

> 拥有更高堆叠顺序的元素总是会处于堆叠顺序较低的元素的前面。

number
auto
inherit

****