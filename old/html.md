# 第一章

## 面试题

​	**网站是位于一个存放网络服务器上的完整信息的集合体。它包含一个或多个网页，这些网页以一定的方式连接在一起，成为一个整体，用来描述一组完整的信息或达到某种期望的宣传效果。**

**网页是网站的组成部分，制作者可以将需要公布的信息按照一定的方式分类，放在每一个网页上，网页里有文字、图像、声音及视频信息等。网页可以看成是一个单独体，是网站的一个元素。**

**首页，也称为主页，它是一个单独的网页，和一般网页一样，可以存放各种信息，同时又是一个特殊的网页，作为整个网站的起始点和汇总点，是浏览者访问一个网站的第一个网页。**

## 一、网站运行

**网站运行需要满足三点：**

​			**1.服务器**

​			**2.域名/IP地址**

​			**3.站点：index.html**

​			**一个基本的网页由html结构层/css表现层/js行为层/img等文件组成**

## 二、万维网

**www是一个基于超文本方式的信息检索服务工具**

**文本开发语言HTML、信息资源的统一定位格式URL和超文本传输信息协议HTTP**

## 三、HTML超文本标记语言

**XML：可扩展标记语言：可以自定义标记（必须是双标记，区分大小写）**

**XHTML：可扩展超文本标记语言：三种不同文本类型**

**XHTML或HTML**

​		**1.过渡型**

​		**2.严格型**

​		**3.框架型**

- **html4.0 pc端**

* **html5.0移动端---header/nav/footer**
* **语义化标签：方便浏览器解析**
* **不同处是h5中新增加了语义化的标签(不需要嵌套)**

## 四、URL

**1.** **URL：统一资源定位器用于描述Internet上资源的位置和访问方式。** **URL中包括协议名：网址/IP/端口号，URI**

[**2. URL：http**](URL:http)**(协议)://www.taobao.com（域名）**

## 五、http超文本传输协议

* **端口号：80**

* **ftp：文件传输协议**

* **smtp：邮件传输协议**

## 六、统一资源定位符格式

**协议名：//网址或IP端口号/URI（统一资源标识符）**

​            **URI构成：**

​            **1.Host(主机名)：定义此域中的主机。**

​            **2.Path(路径)：定义服务的端口号，端口号通常是被省略的			HTTP默认端口号为80**

​            **3.Filename(文件名)：定义的文档名称**

​    		 **URL和URI的区别：URL是包含URI的**

## 七、页面分类

* **页面分为动态页面和静态页面**

* **区别：静态页面不能进行交互 静态页面可以不用上传到服务器上**

## 八、工作原理

* **工作原理：浏览器通过请求指向应用程序URL-URL将请求发送给服务器-服务器执行者创建的制定应用程序-应用程序把结果返回到浏览器**

# 第二章

## 一、html元素

* **Html中只有两种元素：一种是HTML标记，另一种是普通文本。**

## 二、head容器中的标记

### 1.title元素--标题

### 2.link元素--引入css

<link 

### 3.meta元素

1. meta元素--用来做什么【如果有两个一样的加载最后一个】

#### A. name属性

* 用于描述页面

  1. keywords:关键字

  例：```<meta name="keywords" content="网站,网页,web,前端">```

#### B. http-equiv属性

* 主要用于和服务器相关信息

1. refresh：刷新

   例：```<meta http-equiv="refresh" content="5;url=http://www.baidu.com">```**直接替换当前页面，不能返回。**

2. content-type:文本类型

例：```<meta http-equiv="content-type" content="text/html;charset=gb2312/utf-8">```

#### C. content属性

用来解析name和http-equiv

### 4.style元素

用来写css的

### 5.script元素

引入/写js

## 三、Body容器的属性

### 1.背景属性

- bgcolor 背景色

  bgcolor="#f00"

- background 背景图案 （后面接url="图片路径" background="../img/1.jpg"） 

  ```<body background="../img/13.jpg">``` 由于不是同级所以../如果图片在Html目录下直接写background="13.jpg"

### 2.文字属性

* text 正文文字颜色

* link 链接文字颜色

  ```<a href="#">超链接</a>```

* alink 活动链接文字颜色

* vlink 已访问链接颜色

### 3.边距属性

* leftmargin 页面左侧的左边距

  ```<body leftmargin="200px" topmargin="200px">```

* topmargin 页面顶部的边距

# 第三章

## 一、h#标题字

基本语法：

* <h# align="left/center/right">标题文字</h#>

  align属性表示对齐方式

  h#自动换行

## 二、font文字标记 独立标签

基本语法：

```<font face="" size="" color="">文字</font>```	

face表示文字的字体，size表示大小（1-7）,color表示颜色。

```<font face="宋体" size="3" (默认3 值越小字越小) color="#f00">```	size="-1" 在默认的基础上-1即2

## 三、标签的嵌套

```<h3 align="center"><font color="#f00">好好学习，天天向上</font></h3>```

**当标记嵌套不冲突时全显示，当有冲突时按就近原则显示。**

```<font size="5"><h3 align="center"></h3></font>```

## 四、特殊字符

**常见的特殊字符：**

​	空格：&nbsp ; 添加空格

​	版权符：&copy ; 

​	大于号：&gt ;

​	小于号：&lt ; 

​	注册商标：&reg ;

## 五、文字的修饰

* **段落标记和块级标记会自动换行**

  * **行内标记是不会自动换行的标记**        **行内样式根据内容增加他的宽度**

### 1.粗体

```<b></b>```

```<strong></strong>```

### 2.斜体

```<i></i>```

```<em></em>```

### 3.下划线

```<u></u>```

### 4.删除线

```<del></del>```

### 5.地址

```<address></address>```		**段落标记**

### 6.上标

```<sup></sup>```

### 7.下标

```<sub></sub>```	

### 8.等宽标记

```<tt></tt>```

### 9.段落标记

```<p></p>```	**自动换行**	**一个<p>空一行，一个</p>空一行**

### 10.换行标记

```<br>```	

### 11.居中标记

```<center></center>```	**段落标记**

### 12.块标记

```<div></div>```	**段落标记**

```<span></span>```	**行内标记**

### 13.水平分割线

```<hr width="" size="" color="" noshade>```	**单独标记**

width表示分割线的宽度

size表示粗细

color表示颜色	默认是灰色

noshade表示是否有阴影

例：```<hr width="500" size="5" color="#F00">```

### 14.其他段落标记

#### A. 预格式化

```<pre></pre>```	**原样输出**

#### B. 忽略HTML标记

```<xmp>```

​		悯农

锄禾日当午，

汗滴禾下土。

谁知盘中餐，

粒粒皆辛苦。

```</xmp>```

#### C.段落缩进标记

```<blockquote></blockquote>```	**段落标记**

# 第四章 列表【都是块级标记】

## 一、无序列表 

默认为实心的⚪块级标记

`<ul>`

```<li></li>```

`</ul>`

type属性有三个选项：disc(默认为实心圆)、circle（空心圆）、square（方块）**不仅可以给ul加还可以给li加**

`<li></li>`

**嵌套中的第二层为空心圆、第三层为方块**

## 二、有序列表

`<ol></ol>`	块级标记

type属性有五个选项：

*  "1"为阿拉伯数字

*  "A"大写的英文字母

*  "a"小写的英文字母

*  "I"大写的罗马字母

*  "i"小写的罗马字母

**start属性为阿拉伯数字** **只能放在ol中**

## 三、定义列表

```html
<dl>	整个定义列表	
	<dt></dt>放需要解释的词
		<dd></dd>对当前这个词的解释说明
</dl>		
```

## 四、目录列表

```html
<dir>
	<li>第一个列表项</li>
	<li>第一个列表项</li>
</dir>
```

## 五、菜单列表


```html
<menu>
	<li>第一项</li>
	<li>第二项</li>
</menu>
```

# 第五章 超链接

## 一、链接路径

URL:统一资源定位

链接路径分为四种：

* 绝对路径：从站点开始->站点.web58/img/1.jpg

* **相对路径：../img/1.jpg**

* 物理路径：从磁盘开始->E:/web58/img/1.jpg

* 根路径  从主机名开始

## 二、创建超链接

```html
<a href="www.taobao.com" title="我是备注" target="_blank">超链接</a>	默认不跳转任何页面：href="#"	默认只在当前页面跳转
```

### 1.超链接的标记

* 创建超链接的标记是a(anchor,锚),以<a></a>，锚可以指向网络上的任何资源：一张HTML页面，一幅图像，一个声音或视频文件等。

### 2.基本语法

```html
<a href ="资源链接" title="指向链接时显示的文字" target="在指定窗口中打开"></a>
```

说明：

-href:建立链接时，属性"href"定义了这个链接所指的目标地址，也就是路径。理解一个文件到要链接的那个文件之间的路径关系是创建链接的根本。

​	-target:有4个保留的目标名称用作特殊的文档重定向操作。

​			**_blank:在新窗口中打开被链接文档**

​			_self:默认。在相同框架中打开被链接文档

​			_parent:在父框架集中打开被链接文档

​			_top:在顶部窗口中打开被链接文档

​			framename:在制定的框架中打开被链接文档

### 3.内部链接

计算机内部

### 4.外部链接

互联网内的链接

### 5.邮件链接

在HTML页面中简历E-mail链接。

基本语法：

* ```html
  <a href="mailto:E-mail"?subject=邮件主题">描述内容</a>	抄送的意思是同时再发给另一个人
  <a href="mailto:870054481@qq.com?subject=这是一封邮件&cc=3079330791@qq.com&body=内容">超链接</a>
  ```

  &cc=E-mail地址——抄送发件人

  bcc=E-mail地址——暗送收件人

  body=邮件内容

### 6.图片链接

可以为一个图片制作链接

基本语法：

```html
<a href="url" target="目标窗口的打开方式"><img src="图片地址"></a>
<a href="product.html" target="_blank"><img src="../img/12.jpg"></a>
```

### 7.下载文件链接

基本语法：

```html
<a href="url">链接内容</a>
<a href="../img/雅思.zip" target="_blank">下载</a>
```

### 8.书签链接

基本语法：**创建使用的是href，跳转使用的是name。**

在同一页面内要使用书签链接的格式：

```html
<a href="书签名称" target="窗口名称">链接标题</a>
在不同页面之间要使用书签链接的格式（在不同页面中链接的前提是需要指定好链接的页面地址和链接的书签名称）
```

```html
<a href="#想要跳转的页面"></a>		返回顶部:#top
<a name="跳转到的页面"></a>
```

```html
<a href="#top"></a>		
<a name="top"></a>
```

# 第六章 表格

## 一、表格标记

```html
<table>	表格	可以有	先加载table到/table加载完才显示所有的内容
	<caption>表格标题</caption>	显示在表格的上方	单独嵌套在table中
	<th></th>	表头是特殊的单元格	默认居中加粗	可以替代td
		<tr>	行
			<td></td>	列	每个单元格可以有背景颜色和背景图片
		</tr>	
							**单元格内没有内容时不显示**
</table>

<table border="1" width="500" height="800" align="center" background="../img/1.jpg"bordercolor="#ff0">			**表格颜色不能单独设置，背景颜色可以单独设置**
							border用0或1			width="20%" height="100%"
	<caption>学生表</caption>
	<tr align="center" height="40%">
		<th></th>
		<td align="center"></td>
	</tr>
</table>
```

* 在浏览器中显示时，<th>标记的文字按粗体显示，属于表头，td文字按正常字体显示，属于表项。

  align:定义表格中网页的位置

  border:边框粗细

  width：宽度

  height:高度

  bgcolor:背景色

  backgruond:背景图

  bordercolor:边框颜色

## 二、多列合并

```html
<td colspan="n" ></td>
```

说明：colspan="n" 中表示跨多少列

```html
例如：<td colspan="3" ></td>
```

## 三、多行合并

```html
<td rowspan="n"></td>
```

说明：rowspan="n"中n表示跨多少行

```html
例如：<td rowspan="3"></td>
```

## 四、对齐表项

1. 水平对齐方式是用标记<th>、<td>和<tr>的align 属性。

   align属性值分别为：center(居中)、left(左对齐)、right（右对齐）。

2. 垂直对齐的方式则是使用valign属性，valign的属性值分别为：top（靠单元格顶）、bottom(靠单元格底)、middle(靠单元格中)。

## 五、设置单元格间距

基本语法：

```html
<table width="380" border="1" cellspacing="0">
	<tr>
		<td></td>
	</tr>
</table>
```

**<table>标记中的cellspacing属性值可以设置表格中单元格的间距**

## 六、设置单元格边距

**在网页文件中，单元格的边距指单元格中内容与单元格边框的距离**

基本语法：

```html
<table width="380" border="1" cellpadding="0">
	<tr>
		<td></td>
	</tr>
</table>
```

**table标记中的cellpadding属性值可以设置表格中内容与边框之间的距离。**

## 七、表格之间的嵌套

**表格之间的嵌套要放在td中**

#  第七章 多媒体

## 一、插入图片

网页中常用图片格式为GIF、JPEG 、PNG

### 插入图片标记

基本语法：

<img src="url"

**面试题：**

```html
<img src="相对路径">
<img src="../img/1.jpg" width="200" height="200" title="鼠标划入显示此文字" alt="如果加载不出来图片显示这行字" > 
```

**src中的URL是1.直接把图片加载出来2.加载到当前页面中**

**href中的URL是1.何时使用何时跳转 2.href建立链接关系**

border:高版本浏览器中不带边框 低版本浏览器中带边框	**手动加上border="0"**

**img中的属性：**

src：图像URL路径

width:指定图片的显示宽度

height:指定图片的显示高度

hspace:定义图像左侧和右侧的空白。

vspace：定义图像顶部和底部的空白。

align:指定图片的对齐方式

border:指定图片的边框大小

**alt：如果图片无法显示，代替图像的说明文字**

**title:鼠标划入图像所显示的内容**

### 指定图片的对齐方式

<img>标记的align属性用来制定图像与周围元素的对齐方式

基本语法：

```html
<img src="url" align="">
```

align的取值：

left:在水平方向上 向上 左对齐

right:在水平方向上 向上 右对齐

top:图片顶部与同行其他元素顶部对齐

middle:图片中部与同行其他元素中部对齐

bottom:图片底部与同行其他元素底部对齐

### 滚动文字标记

```html
<marquee></marquee>
```

**marquee属性：**

1. **behavior:设置文字的滚动方式**

   scroll：循环滚动（默认值）

   slide:（滚动一次停止）

   alternate:来回交替滚动

2. **direction:设置文字的滚动方向**

   left:由右向左滚动（默认值）

   right:由左向右滚动

   up:由下向上滚动

   down:由上向下滚动

3. bgcolor:设置滚动文字的背景颜色

   英文颜色、#rgb

4. width和height:设置滚动背景的宽和高

   数字:设置背景的绝对面积。

   相对百分比:设置背景相对浏览器窗口的大小

5. hspace和vspace:设置滚动文字背景和周围其他元素的空白间距

   数字：设置背景和周围其他元素的绝对间距

6. loop设置滚动文字的循环次数

   正整数n:文字滚动n次

   infinite:文字滚动无限次（默认值）

7. scrollamount:设置滚动文字每次移动的距离

   数字：文字每次移动的距离

8. scrolldelay:设置滚动文字每次滚动后的间歇时间

   数字（默认单位ms）：滚动文字每次滚动后的间歇时间

**onmouseover="this.stop()" 鼠标划入停止**

**onmouseout="this.start()"鼠标划入开始**

### 背景音乐的标记

基本语法：

```html
<bgsound src="url" loop="">		只能添加声音文件不能显示和调整播放软件的控制面板
```

语法说明：

src指定声音文件的URL来源，即其路径，为必写属性；

loop指定声音文件的循环播放次数，其值为正整数可指定播放次数，值为-1或infinite制定循环播放无限次。

注意：

  使用<bgsound>标记只能添加声音文件，而且也不能显示和调整播放软件的控制面板。

  使用<embed>标记则可以插入各种各样的多媒体，如WMV、MP3、AVI、SWF、MOV、RMVB等格式的多媒体文件。

 基本语法：

```html
  <embed src="url" loop="true/false" autostart="true/false" width="宽" height="高" type="media-type" pluginspage="plugin">
```

语法说明：

src:指定多媒体文件的URL来源，即其路径，为必选属性；

loop:指定声音文件的循环播放次数，值为true可循环播放无限次，值为false只播放一次，false为默认值；

autostart:指定对媒体文件在下载完后是否自动播放;

width和height分别指定多媒体窗口的高和宽。值都为0时类似背景音乐可隐藏面板；

type:指定多媒体的播放类型;

pluginspage:指定插件页面

# 第八章 框架

## 一、框架简介

框架技术可以把浏览器分割成多个小窗口，并且在每个小窗口中，可以显示不同的网页。

## 二、框架的基本结构/属性

```html
<html>
	<head>
		<title>
		</title>
	</head>
		<frameset>	有frameset就不能有body
		    <frame>	单标记
		</frameset>
	</html>
```

框架的设置：

rows属性可定义一个水平分割的窗口框架.可用frameset标记中的rows（水平分割）或cols（垂直分割）属性来分割

基本语法：

```html
<frameset rows="30%,70%">	百分比 <frameset rows="200,*">使用的是像素，*号是剩下的高度
	<frame src="product.html">
	<frame src="contact.html">	想加载几个页面就写几个frame
</frameset>
```

### *******嵌套分割线

```html
<html>
	<head>
		<title>窗口的嵌套分割</title>
	</head>
	<frameset rows="30%,*">
		<frame>
		<frameset cols="20%,*">
		<frame>
		<frame>
		</frameset>
	</frameset>
</html>
```



## 三、框架的边框

```html
<frameset border="n"> 
```

语法说明：n为整数，代表此窗口框架的宽度，单位为像素(px)

## 四、框架的隐藏

  **frameborder属性用于控制窗口框架的周围是否显示框架，此属性可使用在<frameset>标记与<frame>标记中，如果使用在<frameset>标记内，可控制窗口框架的所有子窗口，如果用在<frame>标记中，则只能控制该标记所代表的子窗口。**

基本语法：

```html
<frameset frameborder="0"或"1">
```

**"0"表示不显示边框，"1"表示显示边框，默认值为"1"**

**noresize属性不允许框架移动**

## 五、定义子窗口名称

name属性用来指定窗口的名称，当完成子窗口的名称定义后，可指定超链接的链接目标显示到网页的某个子窗口。

基本语法：

```html
<frame name="子窗口名称">
```

## 六、浮动框架

**可以放在body中** 浮动窗口的宽度就是他的body

```html
<iframe src="product.html" width="200" height="300"></iframe>
```

## 七、框架跟内容的距离

基本语法：**内容距离框架的距离**

```html
<iframe src="url" marginwidth="value" marginheight="value">
```

语法说明：**在html中，利用frame标记中的marginwidth和marginheight属性设置子框架的左右和上下边缘的空白。**

## 八、控制子窗口滚动条

  scrolling属性用于控制窗口框架中是否显示滚动条，使用此属性，可以避免HTML文件因内容过多而无法完全显示。此属性用于<frame>标记中。

基本语法：

```html
<iframe scrolling="yes"或"no"或"auto">
```

yes表示为显示滚动条，no表示不显示 滚动条，auto为自动设置

# 第九章 表单

## 一、表单

表单的概念：

表单可以把来自用户的信息提交给服务器，是网站管理员与浏览器之间的桥梁。

表单有两个重要组成部分：一是描述表单的HTML源代码；二是用于处理用户在表单域中输入的信息的服务器端应用程序客户端脚本，如ASP.NET、JSP等

表单form基本语法：

```html
<form name="" aciton="" method="">

<input>

	<select></select>
	
	<textarea></textarea>
	
</form>
```

name:名称

action:提交到哪个地方的路径  /#刷新	/javascript:;不刷新不提交

**method:当前这个表单的提交方式 两种提交方式：get/post	默认是get	get:1.明文提交/会在地址栏中显示	post:1.密文提交 /不会在地址栏中显示**  **2.使用get提交数据较长是无法提交的 2.post不会   3.get提交一次  3.Post提交两次**

## 二、输入

```html
<input type="">
```

<input>是个单标记，它必须嵌套在表单标记中使用，用于定义一个用户的输入项。

### 单行文本输入框：text

name:当前输入框的名称

maxlength:输入框中最大输入长度

size:输入框的长度。默认20

value:输入框中默认显示的值。不写就是空

### 密码输入框:password

```html
<input name="password"  type="password" maxlength="" size="">
```

### 单选框：radio

```html
<input type="radio" name="sex">男<input type="radio" name="sex" checked>女	checked默认选中其中一个选项
```

**需要加name 使他们成为一对才可以单选**

checked属性：用于指定该选项在初始时是被选中的。

### 复选框:checkbox

```html
<input type="checkbox" name="hobbyone">游戏<input type="checkbox" name="hobbyone">吃饭<input type="checkbox" name="hobbyone">睡觉
```

### 文件选择输入框:file

```html
上传头像：<input type="file" name="file">
```

### 提交按钮:submit和重置按钮reset

当type="submit"时产生一个提交按钮

```html
<input type="submit" value="登录">	按钮上显示登录
```

当type="reset"时产生一个重置按钮，恢复到浏览器默认情况

```html
<input type="reset" value="清空">	按钮上显示清空
```

### 图像按钮：image

```html
<input type="image" name="image" src="url" >	跟提交按钮作用一样
```

### 隐藏框：hidden

```html
<input type="hidden" >
```

### 按钮：button

```html
<input type="button" value="提交">
```

## 三、多行文本输入框：textarea

```html
个人技能：<textarea name="多行文本输入框的文本" rows="设置文本框的行数" cols="设置多行文本输入框的列数" wrap="默认值是自动换行"></textarea>	双标记/多行文本输入框
```

## 四、下拉列表框

```html
<form>
    所在城市：<select name="city">
    			<option value="北京">北京</option>	有几个option就有几个下拉列表项
        		<option value="杭州" selected>杭州</option>	selected默认被选中
    		</select>
</form>
```

size:下拉列表框中显示的数量

name:名称

## 五、button按钮

```html
<button type="submit">按钮</button>
```

**disabled属性 不可用**

## 六、label标签

```html
<label for="username">用户名</label><input name="username" type="text" id="username">
for对应id
```

















