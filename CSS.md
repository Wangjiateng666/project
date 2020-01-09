# 第一章  CSS

**css是层叠样式表。主要控制网页中的样式。它是一种标记语言。**

传统HTML的缺点：

1. 维护困难

2. 标记不足

3. 网页过胖

4. 定位困难

## 1.1 行内式

style作为的是属性

css:  key:"value"

width:"200px";

height:"200px";

```html
<p style="width:200px;color:#ff0;"></p>
```

## 1.2 内嵌式

style作为的是标记

内嵌样式就是将css写在head之间，并用style标记进行声明。


```html
<head>
    <style type="text/css">
        p{
            width:200px;
            height:200px;
            background-color:#0f0;
        }
	</style>
</head>
```



## 1.3 链接式

可以实现html代码和CSS美工的完全分离，便于后期维护。

```html
<link href="1.css" type="text/css" rel="stylesheet">
```

## 1.4 导入式

在style标记中使用@import ("url")导入样式表文件

**link和import区别：**

区别1：link是xhtml标签，除了加载CSS外，还可以定义RSS等其他事务：@import属于CSS范畴，只能加载CSS

区别2：link引用CSS时，在页面载入时同时加载：@import需要页面网页完全载入以后加载

区别3：link是XHTML标签，无兼容问题：@import是在CSS2.1提出的，低版本浏览器不支持。

区别4：link支持使用Javascript控制DOM去改变样式：而@import不支持。



**link：1.用的是href什么时候用什么时候加载	2.作为一个标记 没有兼容性问题**

**import：1.相当于src直接加载		2.有兼容性问题 ie不能使用**

## 1.5 优先级

**行内>内嵌/链接/导入是由顺序决定的（谁放在下面谁最高）**

# 第二章 CSS选择器

CSS中包含了三类基本选择器：分别是标记选择器，类别选择器，ID选择器

## 2.1 标记选择器

1. 和标记名相同名称的选择器
2. 自动应用到相同标记中

写法：

```css
h1{color:red;font-size:25px;}
```

## 2.2 类别选择器

.类别名

1. 类别名用户自己定义
2. 手动应用到不同的标记中

写法：

```css
.one{color:#0000;font-size:25px;}
```

**在html标记中设置class属性的值为选择器名**

```html
.类别名{}

<p class="类别名">
    
</p>
```

**不会自动应用样式，谁用谁有效，不限定标签**



## 2.3 ID选择器

#ID名

1. ID名用户自己定义
2. 手动应用到不同标记中
3. 与类别选择器不同的地方在于同一个ID选择器只能在HTML中使用一次

```html
<p id="id名">	同一个ID选择器只能在HTML使用一次。
    
声明：#ID名{
    
    }    

```

## 2.4 优先级

**ID选择器>类别选择器>标签选择器**

## 2.5 指定标签类别

```css
h1.one{									优先显示.one以为权重最高
	width:200px;
	height:200px;
	background-color:#0ff;
}
.two{
	width:200px;
	height:200px;
	background-color:#0f0;
}
```

两个类别选择器中间用空格隔开

权重：

行内：1000

ID:100

类别/伪类：10

标记：1

h1.one=11	.two=10

## 2.6 选择器声明

### 2.6.1  集体声明

```css
h1,p,.one,#one{
		width:200px;
		height:200px;
		background-color:#f00;
}
```

### 2.6.2 全局声明

**优先级最低**

**使用全局声明，所有的标记都会自动应用该样式**

```css
*{
	background-color:#f00;
}
```

### 2.6.3 选择器嵌套

```css
div p{			div空格p 空格：后代元素

}
```

#### A.父子关系

```css
div>span{	>代表子元素
	background-color:#f00;
}
```

#### B.CSS继承

CSS继承指的是子标记会继承父标记的所有的样式风格，并且还可以在父标记样式类型的基础上再加以修改，产生新的样式，而子标记的样式风格完全不会影响父标记。

1.font-size,font-weight,font-style,font-family	字体

2.text-align,line-height,color	

3.list-style-type	列表

4.visibility	是否可见

5.cursor	鼠标样式

```html
<div>
    <p>
        <span>span1</span>
    </p>
    <span>span2</span>
</div>
<span>span3</span>
```

```css
div{	
	background-color:#f00;
	color:#fff;
}
```



```html
<p><div></div></p>	会分割为两个<p>标记		p标记之间不能嵌套块标记
```

# 第三章	样式

## 3.1 文字样式

### 3.1.1 字体

font-family:字体名称1，字体名称2，.......有多个字体用逗号隔开，最终显示最后一个字体。慎用，系统中没有的字体会默认显示微软雅黑。

### 3.1.2 字体大小

font-size:默认情况下是16px	最小支持12px

1. 相对大小：px(像素,实际是字体占位是多少像素，而不是字的大小)、%、em（倍数）

   

   **em根据父元素的字体大小来改变的**      有像素的属性就可以用em	

```
20*2*20	只跟font-size有关
```

**百分比根据父元素的字体大小仅限于设置字体大小  不能跨属性**

他们之间不能通用

```css
body{
	font-size:20px;
}
div{
	font-size:10px;
}
p{
	font-size:2em;		body
}
```

em跟px之间	在使用em时如果有font-size是所有乘在一起。

```css
body{	
	margin:0;
	padding:0;
	font-size:20px;
}
div{
    font-size:1em;
    background-color:#f00;
    width:20em;
}
```

### 3.1.3 文字颜色

两种表示方式：background-color:#f00;

​						 color:rgb(255,255,255);

### 3.1.4 文字粗细

font-weight:bold (加粗/900) | lighter(100) | normal(400) | 100-900九级粗细

### 3.1.5斜体

font-style:italic | oblique | normal	斜体|倾斜|正常		斜体跟倾斜一样

### 3.1.6 下划线、顶划线和删除线

text-decoration:underline(下划线) | overline(顶划线) | line-through(删除线) | blink(发光) | none(没有线)【用于去掉链接中的下划线】

```css
a{
	text-decoration:none;
	color:#ff0;
}
```

### 3.1.7 英文字母大小写

text-transform: capitalize(首字母大写) | uppercase(全部大写) | lowercase(全部小写);

## 3.2 段落

### 3.2.1 段落对齐方式

水平对齐方式：text-align:left | right | center | justify两端

垂直对齐方式：vertical-align:top | middle | bottom;	必须有vertical-align属性才可以

### 3.2.2 行间距和字间距

行间距：line-height和height值是一样的，表示的是两横文字之间基线的距离。如果给文字加上下划线，那么下划线的位置就是文字的基数。

字间距：letter-spacing设置字与字之间的距离。

------

只设置第一个元素后面的间距即可，能设置right和bottom就不设置其他的。

# 第四章 用CSS设置图片效果

## 4.1 图片边框

border-style:定义边框的样式

border-color:定义边框的颜色

border-width:定义边框的粗细

**分别设置4个边框不同的样式**

* border-left
* border-right
* border-top
* border-bottom

合并书写各个属性的值

## 4.2 图片的缩放

width和height

注：当设置了图片的width属性，而没有设置height属性时，图片会自动的纵横比例缩放，设置了height和width一样。

## 4.3 图片的对齐

1.横向对齐text-align：left | right | center

块级元素居中：margin:0(上下) auto（左右）;

2.纵向对齐 vertical-align:top middle bottom;有效果

```css
body{
	text-align:center;
}
div{
	width:200px;
	height:200px;
	background-color:#f00;
	text-align:center;
	margin:0 auto;
}
```

```css
div{
	width:300px;
	height:200px;
	background-color:#ff0;
	margin:0 auto;
}
img{
    vertical-align:top;
}
```



## 4.4 图文混排

:hover伪类选择器--代表的是鼠标划入的状态

```css
img{
	width:136px;
	height:136px;
}
img:hover{			:hover仅代表鼠标划入的状态
	width:200px;
	height:200px;
}
```

```css
img{
	width:136px;
	height:136px;
}
img:hover{			:hover仅代表鼠标划入的状态
	width:200px;
	height:200px;
	margin-top:-32px;			原地放大
	margin-left:-32px;
}
```

<img src="C:\Users\王加藤\Desktop\1.png" style="zoom:50%;" />

文字环绕：

```css
div{
	width:200px;
	height:200px;
	margin:0 auto;
}
d1{
    width:200px;
    height:200px;
    background-color:#00f;
    float:left;
}
```

float来实现文字环绕:left right让当前浮动的元素脱离文档流，同时会影响后面元素的显示方式，并且后面元素显示时会把当前浮动元素的位置让出来。

浮动元素：水平对齐



设置图片和文字间距：



# 第五章 用CSS设置网页中的背景

## 5.1 页面背景色

background-color:#fff;	rgb(255,255,255)

### 5.1.1用背景色给页面分块

background-color:

## 5.2 背景图片

background-image:url("图片路径")

### 5.2.1背景图的重复

**background-repeat：**

**repeat-x;水平方向重复**

**repeat-y;垂直方向重复**

**no-repeat;不重复**

设置的图片的宽度越小越好，水平方向重复即可

### 5.2.2背景图片的位置

background-position:两个值，top left,top right,top center,center left,center right,center center,bottom left,bottom center,bottom right

​								50%水平,50%垂直

​								0px,0px/-20px,-20px向上向左是负值

### **css sprites、css精灵、雪碧图**

将小的图片拼接成一张大图，使用background-position使用像素定位。

```css
background-image:url("1.jpg");
background-position:-100px -100px;
background-repeat:no-repeat;
```

复合属性：

```css
background:url("1.jpg") no-repeat -100px -100px #f00 fixed;
```

另外写属性时需要单独加image/color等，因为代码是从上往下加载，否则会覆盖上级的设置。

------

**固定背景图片的位置：background-attachment:fixed;**	背景图固定不动 内容动

# 第六章 表格和表单

## 6.1 控制表格

```css
table,td{
	border:#000 solid 1px;
}
table{
    border-collapse:collapse;
}
```

**合并边框：border-collapse：collapse合并/separate分开;**

## 6.2 表格实例：隔行变色

：hover存在兼容性问题

```css
tr:hover{
	background-color:#f00;
}
```

## 6.3 表单

### 必须要加，否则会出现兼容性问题 background:transparent	背景颜色透明

单选框和复选框只能调大小其他设置不可调。

```html
<form action="#" >
	<label></label>
    <label></label>
   
```

```css
input{
	border:none;
    border-bottom:#000 solid 2px;
    width:120px;
    height:50px;
    color:#f00;
    font-size:30px;
    background:transparent;	背景颜色透明	为了解决兼容性问题
}
```

### 下拉列表框

可以加背景颜色，但背景图片只能在下拉列表显示不能在选项中显示

```html
<select>
    <option>北京</option>
    <option>杭州</option>
</select>
```

```css
select{
	background-color:#0ff;
	width:120px;
	font-size;
	border:0;
}
```

# 第七章 超链接

## 7.1丰富的超链接特效

**1.去掉链接的下划线并设置颜色**

```css
text-decoration:none;
color:#ff0;
font-size:30px;
```

**2.伪类选择器来创建动态超链接**

按顺序书写否则会有兼容性问题	**!!!!!!!!!!!顺序： link>visited>hover>active !!!!!!!!**

* :link	正常浏览
* :visited	访问过的状态
* :hover	鼠标划入的状态
* :active	激活的状态

```css
a:link,a:vlink{				两个状态需要一样
	color:#f0f;
	font-size:20px;
	text-decoration:none;
}
```

```css
a:hover{
	color:#0ff;
}
```

鼠标划入按钮颜色改变:需要改变的写在hover、link、visited中，不需要改变的整体写在a中

```css
a{
	width:120px;
	height:50px;
	display:block;
	background-color:#f00;
	text-decoration:none;
	text-align:center;
	line-height:50px;	垂直居中
	color:#fff;
	font-weight:bold;
}
a:link,a:visited{
	background-color:#ff0;
}
a:hover{
    background-color:#ff5;
}
```

## 7.2鼠标特效

```css
cursor:pointer;小手n-resize;上下箭头w-resize;左右箭头；
```

## 7.3页面滚动条

只有在IE浏览器才能生效，其他浏览器不会生效。

scrollbar-arrow-color:向上的小三角的颜色

# 第八章 菜单

## 8.1 列表的符号

list-style-type属性:

* disc实心圆

* circle空心圆

* square正方形

* decimal1，2，3

* upper-alpha A B C

* lower-alpha a b c

* upper-roman 大写罗马数字

* lower-roman 小写罗马数字

* **none 不显示任何符号**

  **项目符号的位置是40px如果需要去掉需写成padding-left:-40px;**     **或者将margin和padding归0；**

### 8.1.1 图片符号

```css
list-style-image:url("1.jpg")
```

插入图片让图片与li中的内容居中对齐

```css
li{
	height:30px;
	line-height:30px;
	list-style-type:none;
	background:url("1.png") no-repeat;
	padding-left:35px;
}
```

## 8.2 制作无需列表的菜单

* display属性

  none	有内容不显示，内容与位置都会隐藏

  block	块级

  inline	行内

  inline-block	行内块

  inherit	从父元素继承display属性的值

  visibility:hidden只隐藏内容不隐藏位置/visible

### 8.2.1 侧导航

li的宽高已经固定住了，超出的部分就不会显示，高度是由a来决定的。在a里面设置。

* **实现测导航的步骤：**

1. 先把列表的项目符号去掉
2. 给li设置上宽高
3. 给a转换成块级元素
4. 设置a的样式
5. 需要改变的样式放在a:link,a:visited，a:hover中

### 8.2.2 横向导航

直接float:left;

居中直接给ul设置宽度因为ul是li的父元素，width:480px;

子元素浮动父元素没有宽度和高度，因为子元素脱离文档流。

**实现横向导航的步骤：**

1. 先把列表的项目符号去掉（给ul设置宽度同时加上margin:0 auto;）
2. 给li设置上宽高（给li加上浮动）
3. 给a转换成块级元素
4. 设置a的样式
5. 需要改变的样式放在a:link,a:visited,a:hover中

**使导航栏长度加长：将导航放在div中给div设置高度**	

#### 常见的例子：

例1：鼠标划入文字变色

例2：鼠标划入背景变色/背景与字体交换颜色

例3：鼠标划入替换背景图片

例4：圆角导航

### 8.2.3 带图标的导航

**html部分：**

```html
<div>
    <ul id="u2">
        <li><a>天猫</a></li>
        <li><a>聚划算</a></li>
        <li><a>天猫超市</a></li>
        <li><a>淘抢购</a></li>
        <li><a>电器城</a></li>
        <li><a>司法拍卖</a></li>
    </ul>
    </div>
```

**CSS部分：**

```css
ul{
    list-style-type:none;
    height:100px;
    width:480px;                                /*居中计算宽度*/
    margin:0 auto;
    padding-top:50px;
}
li{
    float:left;
    height:40px;
    width:80px;
}
a{
    display:block;
    height:23px;
    margin-top:17px;
    text-decoration:none;
    background-color:#FF7F00;
    text-align:center;
}
div{
    height:100px;
}
ul>li:hover{
    background:url("aliwawa.jpg") no-repeat 25px 2px;
}
```

### 8.2.4 二级导航栏

```
+下一个兄弟：a下一个是ul才能被找到
```

```
>：规定范围内找符合条件的元素
```

行内元素不能嵌套块级元素

```css
#nav a:hover+ul{
    display:block;
}
```

二级菜单例题:html部分

```html
        <ul id="nav">
            <li class="two"><a>首页</a></li>
            <li class="two">
                <a>产品中心</a>
                <ul class="one">
                    <li><a>橘子</a></li>
                    <li><a>汽水</a></li>
                    <li><a>垃圾食品</a></li>
                    <li><a>炸鸡</a></li>
                </ul>
            </li>
            <li class="two"><a>客户中心</a></li>
            <li class="two"><a>联系我们</a></li>
        </ul>
```

CSS部分：

```css
ul{
    list-style-type:none;
    cursor: default;
}
#nav .two{
    background-color:rgb(0, 255, 234);
    width:120px;
}
#nav ul{
    padding:0px;
    display:none;
}
#nav a:hover{
    font-size:30px;
}
#nav a{
    display:block;
    width:120px;
    text-align:center;
    text-decoration: none;
    height:50px;
    line-height:50px;
}
#nav a:hover+ul{
    display:block;
    background-color:rgb(255, 153, 0);
    width:120px;
}
```

# 第九章 滤镜

## 9.1 透明度

0-1;只能取整例如：0.5为半透明，0全透明，1完全不透明

```css
opacity:0;
```

# 第十章

## 10.1 div与span的区别

* **div是一个块级元素，它包围的元素会自动换行。**

* **span仅仅是一个行内元素，在它的前后不会换行。**

* **span没有结构上的意义，纯粹是为了应用样式，当其他的行内样式都不合适时，就可以使用span元素。**

* **div可以包含span,但是span不能包含div**

## 10.2 块和行内的强制转换

**块级不会受空格的影响，行内会受影响。**

块级元素：address,center,div,dl,form,h1~h6,hr,ol,p,table,ul;

行内元素：a,strong,br,em,img,input,label,select,span,sub,sup,textarea

### **10.2.1 块级元素：**

1. **总是从新的一行上开始。**
2. **高度、宽度都是可控的。**
3. **宽度缺省的时候他的容器宽度为100%**
4. **块级元素中可以可以包含块级元素和行内元素。**

### **10.2.2 行内元素：**

1. **和其他元素都在一行上。**
2. **高度，宽度以及内边距都是不可控的。**
3. **宽高就是他的文字或图片的高度，不可改变。**
4. **行内元素只能是行内元素，不能包含块级元素。**

### 10.2.3 行内元素与块级元素的转换：

1. **display:block将目标转换为块**
2. **display:inline将目标转换为行内**
3. **display:inline-block 行内块**

## 10.3 盒子模型

### 10.3.1 盒子模型的概念

​	一个盒子由content（内容），border（边框），padding（间隙），margin（间隔）这四个部分组成，所以一个盒子模型的实际宽度或高度是由content+padding+border+margin组成的。在css可以通过设定width和height来控制content的大小。

宽：margin-left+border-left+padding-left+content+padding-right+border-right+margin-right

------

### 10.3.2 border边框

border就是边框，边框的外围就是元素的最外围，边框也有宽度，所以就算元素实际宽高的时候也要将边框的宽度就算在内。

**border的属性主要有三个：color（颜色）、width（粗细）、style（样式）**

边框的样式：none,hidden,dotted,dashed,solid,double,groove,ridge,inset,outset

**主要样式:dotted、solid、double、**

如果要设置某一个边框则使用border-bottom(left、right、top)来完成。

------

**正常情况下：背景颜色是包含边框的。**

border-left-color:在中间加哪个方向就是哪个方向。

```css
复合属性：border:10px solid  #f00;
```

三角形制作：

```html
    <div>div1</div>
    <div class="d1"></div>
```

```css
div{
    border-left:solid 10px #f00;
}
.d1{
    width:0px;
    border:solid 5px #fff;
    border-left-color:#0ff;
    border-bottom-color:#f00;
    border-right-color:#ff0;
}
```

### 10.3.3 padding

* **padding是用于控制content与border之间的距离的。**
* **我们可以给padding的不同位置设置不同的值**

**padding:一个值是所有的边框 ，两个值是上下和左右，三个值是上，左右，下，四是顺时针上右下左**

* **给行内元素设置margin-top和margin-bottom没有效果，需要给父元素设置padding值。**

* **块级元素不受影响**

### 10.3.4 margin

**行内元素的margin值的计算方式是margin-right+margin-left**

**块级元素的margin值的计算方式是谁大取谁**

**样式重置：所有元素都会有自己的padding和margin的值，需要将他们归零。**

```css
html,body,div,a,ul,li,img,span{
	margin:0;
    padding:0;
}
```

兼容性：w3c标准：宽高往外扩比实际的多

​				IE往里面缩：实际设置多少就是多少

## 10.4 元素的定位

主要属性：float、position、z-index

### 10.4.1 float浮动

**float:right右;left左;none无;**

1. 父元素中有两个子元素，第一个子元素左浮动，会影响父元素及第二个元素。
2. 第二个元素左浮动，不会影响第一个子元素。
3. 两个子元素都左浮动，两个元素将并排向父元素的左侧靠近。

### 10.4.2 clear清除浮动

**1.clear：谁受影响给谁加**

```css
clear:left左;right右;both两边;	既有left/right就写both;
```

**2.给父元素加一个高度也可以清除浮动**

### 10.4.3 position定位

position用来指定块级元素相对于夫块位置和相对于它本身的位置

可以脱离文档流

position属性一共有四个值：static(默认)、absolute、relativer和fixed。

position定位要配合top、right、bottom、left属性进行定位，值可以是像素也可以是百分数。

#### 1.absolute绝对定位：

相对于当前窗口来定位

```css
position:absolute;
top:0px;
left:0px;
```

**父元素没有定位，相对于窗口定位。父元素有定位，相对于父元素。**

没有设置宽高时，父元素的宽高由子元素的宽高撑起来。

元素是可以重叠的。

#### 2.relative相对定位

元素不能重叠。保留最一开始的位置。

不管父元素有没有定位，始终相对于自己本身定位，保留之前的位置。

### **绝对定位和相对定位的区别：**

1. 相对定位是相对于自己本身的定位，元素是不可以重叠的。父元素高度由子元素决定，宽度依然是父元素本身。保留自己一开始的位置。
2. 绝对定位相对于窗口定位的，如果父元素没有定位的情况下，相对于窗口来定位，父元素的宽高由子元素决定，如果父元素有定位的情况下，相对于父元素定位，不管父元素是什么定位都一样，宽高依然由子元素决定。绝对定位后就失去自己的位置。可以重叠。

* 如果父元素absolute，子元素relative，那么父元素宽高就是子元素宽高。


```css
#d1{
	background-color:#ff0;
    position:absolute;
    top:10px;
    left:10px;
}
#d2{
    width:200px;
    height:200px;
    background-color:#0ff;
    position:relative;
    top:10px;
    left:10px;
}
```

* 如果父元素relative，子元素absolute，那么父元素宽度是原来的宽度，因为子元素没有位置。

```css
#d1{
	background-color:#ff0;
    position:absolute;
    top:10px;
    left:10px;
}
#d2{
    width:200px;
    height:200px;
    background-color:#0ff;
    position:relative;
    top:10px;
    left:10px;
}
```

#### 3.fixed固定定位

与绝对定位一样，是**相对于窗口进行定位**的，不过他不会随着滚动条的滚动而移动，搭配top,bottom,left,right来调整位置。**可以重叠**

#### 4.z-index空间定位

用来调整重叠的顺序，随着数值的增大而优先显示，垂直于页面的方向为z轴。

```css
#d1{
	background-color:#ff0;
    position:absolute;
    top:0px;
    left:0px;
    z-index:1;
}
#d2{
    width:200px;
    height:200px;
    background-color:#0ff;
    position:absolute;
    top:0px;
    left:0px;
}
```

如果z-index的值是一样的那么谁最后加载出现谁

#### 5.overflow

溢出一个元素框

* visible默认值

* hidden内容被修剪，其余内容是不可见的

* scroll内容被修剪，超不超出都会显示滚动条，加上滚动条的合起来为所设定的宽度

* Auto如果内容被修剪，超出会显示滚动条，加上滚动条的合起来为所设定的宽度

#### overflow清除浮动的方式

给**父元素**直接加overflow:hidden,auto,scroll来清除浮动

#### bfc块级格式化上下文

父元素在计算高度的时候，会把浮动的子元素的高度计算进去。

# 第十一章 css+div布局

固定布局	pc端

## 1.PC端 固定浮动布局float

float:不随窗口变化而变化，缩放窗口不回影响网页布局，采用margin:0 auto方式居中

### 自适应两列：

左侧浮动确定宽高，右侧确定高度并且不给浮动，自动适应父元素所设置的宽度。

```html
<div id="header">header</div>
<div id="nav">nav</div>
<div id="banner">banner</div>
<div id="content">content</div>
	<div id="left">left</div>
	<div id="right">right</div>
<div id="footer">footer</div>
```

```css
div{
    width:900;
    margin:0 auto;
    text-align:center;
}
#header{
    height:100px;
    background-color:#f00;
}
#nav{
    height:50px;
    background-color:#f00;
}
#banner{
    height:400px;
    background-color:#00f;
}
#left{
    width:300px;
    height:600px;
    background-color:#0f0;
    float:left;
}
#right{
    width:600px;
    height:600px;
    background-color:#0ff;
    /*自适应*/
}
#footer{
    clear:both;
    height:150px;
    background-color:#ff0;
}
```



### 自适应三列：

不浮动的放最后面，CSS的加载顺序根据html顺序加载

```html
<div id="header">header</div>
<div id="nav">nav</div>
<div id="banner">banner</div>
<div id="content">content</div>
	<div id="left">left</div>
	<div id="right">right</div>
	<div id="middle">middle</div>	/*把不浮动的Middle写在最后，最后加载*/
<div id="footer">footer</div>
```

```css
div{
    width:900;
    margin:0 auto;
    text-align:center;
}
#header{
    height:100px;
    background-color:#f00;
}
#nav{
    height:50px;
    background-color:#f00;
}
#banner{
    height:400px;
    background-color:#00f;
}
#left{
    width:300px;
    height:600px;
    background-color:#0f0;
    float:left;		/*左浮动固定*/
}
#middle{
    height:600px;
    background-color:#f0f;			/*中间自适应*/
}
#right{
    width:200px;
    height:600px;
    background-color:#0ff;
    float:right;	/*右浮动固定*/
}
#footer{
    clear:both;
    height:150px;
    background-color:#ff0;
}
```

## 2.PC端 固定定位布局position

不随窗口变化而变化，主要使用position:absolute；进行定位，缩放窗口不会影响网页布局，采用position:absolute拉回方式进行居中。

left:50%

margin-left:-450px;

top:每个独立设置下面的是上面的累加和。

三列，**不能自适应**

```css
body,div{
    margin:0px;
    padding:0px;
}
div{
    width:900px;
    margin:0 auto;
    text-align:center;
    position:absolute;
    margin-left:-450px;
    left:50%;
}
#header{
    height:100px;
    background-color: #f00;
    top:0px;
}
#nav{
    height:50px;
    background-color: #0f0;
    top:100px;
}
#banner{
    height:400px;
    background-color: #00f;
    top:150px;
}
#left{
    width:200px;
    height:400px;
    background-color: #f0f;
    top:550px;   
}
#middle{
    height:400px;
    width:200px;
    background-color: #000;
    color:#fff;
    top:550px;
    margin-left:-250px;
}
#right{
    width:500px;
    height:400px;
    background-color: #ff0;
    top:550px;
    margin-left:-50px;
}
#footer{
    clear:both;
    height:50px;
    background-color: #0ff;
    top:950px;
}
```

## 3.移动端 流体布局



```css
#nav{
	height:100px;
	background-color:#555;
}
#nav ul{
	list-style-type:none;
	height:100px;
	width:100%;
}
#nav li{
	display:block;
	width:25%;
	height:100px;
	float:left;
}
#nav a{
	margin:0 auto;
	display: block;
	height:100px;
	width:100%;
	float:left;
	color:#fff;
	line-height:100px;
	text-decoration:none;
}
```

```css
#banner{
	height:500px;
	background-color:#222;
	background-image: url("4.jpg");
}
#banner ul{
	position:fixed;
	width:100px;
	position:absolute;
	top:680px;
	left:50%;
	margin-left:-50%;
	list-style-type: none;
	margin:0 auto;
}
#banner span{
	width:20px;
	height:20px;
	display:block;
	background-color: #fff;
	float:left;
	margin-right:5px;
	border-radius: 10px;
}
#banner span.active{
	background-color: #ff0;
}
```

# 第十二章 CSS兼容性总结

## 12.1 浏览器内核

Trident内核（IE内核）

​			IE 360 猎豹

Gecko内核（firefox内核）

Webkit内核（safari内核，Chrome内核）

​			360极速浏览器，搜狗高速浏览器，safari浏览器，Chrome浏览器

Presto内核（Opera内核）

## 12.2 CSS reset

通过重置默认样式解决最基本的兼容性问题

**margin,padding,a下划线,ul,ol,img去掉边框**

## 12.3 CSS HACK

我们把针对不同浏览器/不同版本写相应的CSS code的过程叫做CSS Hack

**CSS HACK有三种表现形式，CSS属性前缀法，选择器前缀法以及IE条件注释法（即HTML头部引用if IE）**

### 方式一： 条件注释法

只能在IE下生效：

```html
<!--[if IE]>在IE浏览器显示<link rel="stylesheet" href="1.css"><![endif]-->
```

只能在IE 6下生效:

```html
<!--[if IE 6]>这段文字只在IE6浏览器上显示<![endif]-->
```

只能在IE6以上版本生效：

```html
<!--[if gte IE 6]>这段文字只在IE6以上（包括）版本IE浏览器显示<![endif]-->
```

只在IE8上不生效：

```html
<!--[if !IE 8]>这段文字在非IE8浏览器显示<![endif]-->
```

非IE浏览器生效：

```html
<!--[if !IE]>这段文字只能在非IE浏览器显示<![endif]-->
```

### 方式二：属性前缀法第一种

```CSS
*  IE6IE7	例子:*color:#0ff;
_  IE5IE6 例子：_background:#fff;
\9 IE6~IE11都能识别，火狐与谷歌不能识别。例子：height:120px\9;
\0 IE5~IE11能识别,火狐与谷歌不能识别
\9\0 IE8~IE10能识别,火狐与谷歌不能识别
```

-webkit-background:#f00;	chrome

-moz-background:#f00;	 firefox

-o-background:#f00;	Opera

-ms-background:#f00;	IE

background:#f00;

### 方式二：属性前缀法第二种

比行内的优先级还要高，用时谨慎！！

```css
!important;	IE6不识别，其他都可以
```

注意：IE6不认识!important的优先级，但不代表不认识带!important的样式属性

```
例子：demo{
	color:red!important;	除了ie6其他浏览器会认为红色优先级最高，显示红色字体
	color:green;	ie6浏览器则顺序读取css所以显示绿色
}
```

## 补充：IE6 BUG

#### ***1.双边距问题

产生时机：父元素设置浮动，子元素也设置浮动并且子元素设置margin-left,就会出现margin-left双倍的问题。

解决方法：给子元素加上display：inline;

#### ***2.三像素BUG

产生时机：两个元素，第一个元素设置左浮动float：left;第二个元素不设置浮动，造成之间产生3px的间隔。

解决方法：给第二个元素加上左浮动float：left;

#### 3.图片下方间隙

所有浏览器都会遇到此问题

产生时机：图像下方添加块级元素，之间就会产生间隔，firefox,ie,chrome中都存在这种问题

解决方法：给图片标记添加display:block;或者设置vertical-align

#### 4.空元素高度问题

IE

产生时机：如果一个元素中没有任何内容，当样式中为这个元素设置了0-19px之间的高度时，此元素的高度始终为19px

解决方法：给空元素设置font-size:0;或者加overflow:hidden;

#### 5.超链接文字动态效果的顺序问题

产生时机：没有按照顺序设置样式

解决方法：按照顺序写 a:link a:visited a:hover a:active

#### ***6.li外边距问题

产生时机：当li标记中最后一个子元素设置浮动后会导致，每个li之间会产生3px的间距。

解决方法：给<li>标记添加css样式vertical-align:top;

#### 7.png图片背景透明问题

产生时机：ie6不支持png格式的图片透明效果

解决方法：使用ie条件注释添加Js插件

```html
<!--[if IE 6.0]>
<script type="text/javascript" src="DD_belatedPNG.js"></script>
<script type="text/javascript">
DD_belatedPNG.fix('img');
</script>
<![endif]-->
```

background-color:rgba(0,0,255,0.5);

## 12.4 CSS优先级

**1.!important的优先级是最高的，单出现冲突时则需比较"四位数"。**

**2.优先级相同时，则采用就近原则；**

**3.继承得来的属性，其优先级最低；**

























































































































