# HTML5

## 第一章 

### 1.1 网站运行三要素：服务器、站点、域名/IP地址

http:超文本传输协议：用来传输超文本的

1. 在地址栏输入域名之后，服务器会接收域名，在接收域名之前会对当前你输入的这个域名先进行解析（浏览器和服务器之间不能直接进行通信）使用的是DNS服务进行解析的
2. 解析完域名之后因为服务器有很多个，然后需要确定是在哪一个服务器上
3. 然后通过TCP/IP协议进行链接的建立，在建立链接的过程当中需要三次握手，这种情况下才能接收到（服务器），第一次握手：先需要确定的是请求链接，第二次握手：服务器端确认请求，第三次握手：客户端（浏览器端）确认请求
4. 建立完链接之后就可以进行传输了，客户端会把域名传输给服务器端，服务器端会返回HTML内容给客户端
5. 客户端接收和解析

### 1.2 URL统一资源定位符



### 1.3 静态页面

后缀名.html，.htm，.shtml，.xml

### 1.4 动态页面

后缀名.php，.aspx，.asp，.jsp等

### 1.5 XML语言

它可以用来标记数据、定义数据类型，是一种允许用户对自己的标记语言进行定义的源语言。

### 1.6 XHTML语言

可扩展超文本标记语言。

比HTML的语言要严格，区分大小写

### 1.7 html5使用方向

网站(pc端/移动端)，微信公众号，html5场景，混合式app，html5游戏等等

#### html5兼容性

移动端完全支持

PC端一部分支持(最新版本的chorme，firefox，opear全部支持，IE9以上部分支持)

### 1.8 html5优势/功能/特点

* html5的两大特点：强化了web网页的表现性能。追加了本地数据库等Web应用的功能

* 面试题：**1. doctype的作用是什么？什么是严格模式和混杂模式？以及如何触发严格模式和混杂模式？**

html中有doctype:用来定义文档类型，框架型，严谨型，过渡型。

严格模式就是在定义文档类型的时候，将文档类型直接定义出来了。

混杂模式就是没有doctype

触发的话使用的是doctype来进行触发的

**2.h5优势是什么？新增了哪些功能？新增了哪些标记？废弃了哪些标记？**

优势：化繁为简，向下兼容，语义化标签，实用性，用户优先，通用访问

新增功能：Html原生功能：canvas绘图，跨文本消息传递，地理位置，本地存储，本地数据库

新增标记：header,section,article,footer,audio,video,source,canvas

废弃的标记：center,font,big,bgsound,marquee,frame

**3.从输入网址到显示页面的过程**

参考1.1



## 第二章 HTML新增元素及属性

### 2.1 新增元素和属性

```html
<bdo dir="rtl">好好学习，天天向上</bdo> 行内
<abbr title="朗科网络">Link</abbr>缩写title里面写的是全称 行内
<blockquote cite="http://www.baidu.com">里面的内容会缩进</blockquote>块级  代表的是引用的网址
<q>你今天快乐了没</q>会自动给语句加上双引号  行内
<cite>哈哈哈哈哈</cite>用于表示文章标题的，默认显示斜体  行内
<code>document.getElementById("btn")</code>表示一段计算机代码  行内
<dfn>优雅降级，渐进增强</dfn>用来定义专业术语的  浏览器用粗体或斜体来表示  行内
<ins datetime="2019-12-18"></ins>定义插入的文本 默认带下划线  行内 datetime当前这个文本插入的时间
通常与del一起用
<del></del>删除线  行内
```

```html
<img> 
<area shape="rect矩形/circle圆形/poly多边形">shape    coords定义点击坐标的     圆形：coords="x,y,r"	矩形="x1,y1,x2,y2";左上角和右下角坐标 多边形coords="x1,y1,x2,y2,x3,y3"坐标表示多边形每个顶点的坐标
<map name="mapname">:用于定义图片映射，该元素包含一个或多个<area>单标记 子元素
```



### 2.2  通用属性

```html
1. contenteditable=""
当值为true时，浏览器允许用户 直接编辑html元素内容并且具有可继承性，除非将值该为false(不是所有浏览器)
2. html5使用isContenteditable属性，如果可以编辑返回值为true，否则返回false
3. designmode 相当于一个全局的contendeditable，如果把整个页面的designmode属性设置为on，该页面上所有可支持contenteditable的元素都可以编程编辑状态
默认为off
一般用document.designMode="on"在body开启(onload时间加载)
4.hidden
标记当中带有hidden属性的组件都会被隐藏并且不会保留所占用空间同CSS样式里display:none一样
spellcheck 拼写错误
只能给input和textare加这个属性
<input type="text" spellcheck="true">
为true时，浏览器会负责对用户输入的文本内容执行输入检查，如果检查不通过，浏览器会对拼写错的单词进行提示
***大部分浏览器不支持此属性***
```

### 2.3 文档结构元素

都是块级元素

```html
<article></article>用于指定页面上独立、完整的一篇文章或区域
内部可以包含一下几个元素
<section></section>section：对页面进行分块的
	section和article的区别在与section侧重于文章分块，article侧重于整篇文章
<nav></nav>nav 用于定义页面上的导航
<aside></aside>aside用于定义当前页面或者当前文章的负数信息，推荐aside元素使用css渲染称侧导航
<header></header>header文章头部新，可以包含块级或行内元素
<footer></footer>footer版本信息，作者授权等
<mark></mark>mark标记重点 黄色显示
<time></time>time用来标记时间的 有个属性datetime="9:00"
<meter value="0.4" max="1" min="0"></meter> meter表示一个技术仪表 value是仪表当前值 min最小值，默认为0,max最大值，默认1，low指定范围的最小值，该值必须大于min，high指定范围的最大值，该值必须小于max optimum:指定有效的仪表范围的最佳值
超出之后显示黄色 正常范围内绿色 d
<progress value="80" max="100" min="0"></progress>进度条   value里面所占的  max:指定进度条完成时的值
```

```css
1.进度条
progress{
    width: 168px;
    height: 5px;
    border-radius: 2px;
}
/* 表示总长度背景色 */
progress::-webkit-progress-bar{     
    background-color: #f2f2f2;
    border-radius: 2px;
}
 /* 表示已完成进度背景色 */
progress::-webkit-progress-value{
    background: #28cfc1;
    border-radius:2px; 
}
```

### 2.4 音视频

HTML5能在完全脱离插件的情况下播放音视频，但是不是所有格式都支持。

#### 2.4.1 HTML5支持的视频格式

```
Ogg=带有Theora视频编码+Vorbis音频编码的Ogg文件
	支持的浏览器FireFox、Chorme、Opear
MEPG4=带有H.264视频编码+AAC音频编码的MPEG4文件
	支持的浏览器S、C
WebM=带有VP8视频编码+Vorbis音频编码的WebM格式
	支持的浏览器I、F、C、O
```

#### 2.4.2 video的使用

```html
<video src="文件地址" controls="controls"></video>

<video src="文件地址" controls="controls">您的浏览器暂不支持video标签。播放视频</video>

<video controls="controls" width="300">
	<source src="move.ogg" type="video/ogg">
    <source src="move.mp4" type="video/mp4">
    您的浏览器暂不支持video标签，播放视频
</video>
```

#### 2.4.3 video的常见属性

```css
属性			值				描述
Autoplay	Autoplay		视频就绪自动播放
Controls	Controls		向用户显示播放控件
Width		Pixels(像素)	   设置播放器宽度
Height		Pixels(像素)	   设置播放器高度
Loop		Loop			播放完是否继续播放该视频，循环播放
Preload		Preload			是否等加载完再播放
Src			url			    视频url地址
Poster		Imgurl			加载等待的画面图片
Autobuffer	Autobuffer		 设置为浏览器缓冲方式，不设置autoplay才有效
```

#### 2.4.4 video的API方法

```css
方法				属性				事件
play()			 currentSrc			play			开始
pause()			 currentTime		pause			暂停
load()			 videoWidth			progress
canPlayType		  videoHeight		 error
```

```javascript
控制视频开始与暂停
document.getElementById("btn").onclick=function(){
    document.getElementById("vid").play();
}
document.getElementById("btn").onclick=function(){
    document.getElementById("vid").pause();
}
```

```css
										全屏						退出全屏
Webkit(safari5.1/chorme 15)	  element.webkitRequestFullScreen();  document.webkitCancelFullScreen();
Firefox(works in nightly)	  element.mozRequestFullScreen();	 document.mozCancelFullScreen();
W3C提议					  element.requestFullScreen();		 document.exitFullscreen();
```

```css
属性				说明
audioTracks		  返回可用的音轨列表(Multiple TrackList对象)
autoplay		  媒体加载后自动播放
buffered		  返回缓冲部件的时间范围(TimeRanges对象)
controller		  返回当前的媒体控制器(MediaController对象)
controls		  显示播控控件
crossOrigin		  CORS设置
currentSrc		  返回当前媒体的URL
currentTime		  当前播放的时间，单位秒(快进快退10秒)
defaultMuted	  缺省是否静音
defaultPlaybackRate		播控的缺省倍速
```

```javascript
document.getElementById("btn").onclick=function(){
	document.getElementById("vid").currentTime-=5	-=快退5秒  +=快进5秒
}
```

```css
属性						说明
duration				  返回媒体的播放总时长，单位/秒
ended					  返回当前播放是否结束标志
error					  返回当前播放的错误状态
initialTime				  返回初始播放的位置
loop					 是否循环播放
mediaGroup				  当前音视频所属媒体组(用来链接多个音视频标签)
muted					 是否静音
networkState			  返回当前网络状态
paused					 是否暂停
playbackRate			  播放的倍速(加速、减速播放)
played					 当前播放部件已经播放的时间范围(TimeRanges对象)
preload					 页面加载时是否同时加载音视频
readyState				 返回当前的准备状态
seekable				 返回当前可跳转部件的时间范围(TimeRanges对象)
seeking					 返回用户是否做了跳转操作
src						 当前音视频源的URL
startOffsetTime			  返回当前的时间偏移(Date对象)
textTracks				 返回可用的文本轨迹(TextTrackList对象)
videoTracks				 返回可用的视频轨迹(VideoTrackList对象)
volume					音量值				取值范围0-1
```

```javascript
是否静音
1.document.getElementById("btn").onclick=function(){
    document.getElementById("vid").muted=true;
}
2.倍速减速播放
document.getElementById("btn").onclick=function(){
    document.getElementById("vid").playbackRate/=3;			*的话是加速 /是减速
}
3.音量加减
document.getElementById("btn").onclick=function(){
    document.getElementById("vid").volume+=0.2			+=音量加  -=音量减
}
4.播放暂停
document.getElementById("btn").onclick=function(){
    if(this.value=="暂停"){
        document.getElementById("vid").pause();
        this.value="播放";
    }else{
        document.getElementById("vid").play();
        this.value="暂停";
    }
}
5.音量条
document.getElementById("volumeBig").onclick=function(){
  document.getElementById("s").style.height=parseInt(document.getElementById("s").style.height)+10+"px";
}
document.getElementById("volumeSmall").onclick=function(){
  document.getElementById("s").style.height=parseInt(document.getElementById("s").style.height)-10+"px";
}
<button id="volumeBig">+</button>
<div id="volumeControl"><span id="s" style="height:0px"></span></div>
<button id="volumeSmall">-</button>
```

#### 2.4.5 Video的常用事件

**以下所有事件绑定方法都是用对象.addEventListen(事件名，处理函数，false)**

* ratechange			当倍速改变的时候会在视频上弹出来一个提示当前倍速的信息
* playing                  当视频缓冲不过来的时候 提示切换清晰度
* error                      视频出错加载不出来

```css
事件							描述
abort						当音视频加载被异常终止时产生该事件
canplay						当浏览器可以开始播放该音视频时产生该事件
canplaythrough		当浏览器可以开始播放该音视频到结束而无需因缓冲而停止时产生该事件
durationchange				当媒体的总时长改变时产生该事件
emptied						当前播放列表为空时产生该事件
ended						当前播放列表结束时产生该事件
error						当加载媒体发生错误时产生该事件
loadeddata					 当加载媒体数据时产生该事件
loadedmetadata				 当收到总时长，分辨率和字轨等metadata时产生该事件
loadstart					当开始查找媒体数据时产生该事件

pause						暂停
play						播放
playing						当媒体从因缓冲而引起的暂停和停止恢复到播放时产生该事件
progress					当获取到媒体数据时产生该事件
ratechange					当播放倍数改变时产生该事件
seeked						当用户完成跳转时产生该事件
seeking						当用户正执行跳转时操作的时候产生该事件
stalled						当试图获取媒体数据，但数据还不可用时产生该事件
suspend						当获取不到数据时产生该事件
timeupdate					当前播放位置发生改变时产生该事件
volumechange				当前音量发生改变时产生该事件
waiting						当视频因缓冲下一帧而停止时产生该事件
```

```javascript
1.测试视频是否播放
document.getElementById("vid").addEventListener("play",function(){
    console.log("视频播放了");
},false)
```

#### 2.4.6 HTML5支持的音频格式

* Ogg				免费支持的浏览器：C  F  O
* MP3				收费支持的浏览器：I    C   S
* Wav				收费支持的浏览器：F    O   S

#### 2.4.7 audio的使用

如果不加controls的情况下可以作为背景音乐

音频与视频的用法是一样的 只有标签不同

```html
<audio src=" 文件地址" controls="controls"></audio>
<audio src="文件地址" controls="controls">您的浏览器暂不支持audio标签。播放视频</audio>

<audio controls="controls" >
<source src="happy.MP3" type="video/mpeg">
<source src="happy.ogg" type="video/ogg">
您的浏览器暂不支持audio标签。播放视频
</audio>
```

```css
属性					值					描述
autoplay			autoplay			如果出现该属性，则音频在就绪后马上播放。
controls			controls			如果出现该属性，则向用户显示控件，比如播放按钮。
loop				loop				如果出现该属性，则每当音频结束时重新开始播放。
preload	preload		如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果用"autoplay",则忽略该属性。
src					url					要播放的音频的URL。
```

## 第四章 表单

### 4.1 表单元素

* label标签为input元素定义标注

  label for属性

```html
<label for= "username">用户名:</ label><input type= " text" id="username">
label中的for与input中的id属性应该相同
```

* button

* datalist    作为一个下拉列表与select不同的是它可以输入内容  当滑入的时候会显示下拉小箭头

  ```html
  
  <input list="city">	两个里面要写的一致list与id
  <datalist id="city">
  	<option value="广州"></option>
      <option value="广州"></option>
      <option value="广州"></option>
      <option value="广州"></option>
      <option value="广州"></option>
  </datalist>
  ```

### 4.2 HTML表单属性

**不能放在form标签中使用**

* placeholder属性提供可描述输入字段预期值的提示信息

  当你输入的时候里面的内容就消失了

```html
<input type="text" placeholder="请输入用户名">
<input type="text" placeholder="请输入密码">
```

input类型

* color 用于选取颜色

  ```
  获取颜色的时候使用的是value
  onchange属性
  ```

  ```javascript
  更改主题颜色
  document.getElementById("co").onchange=function(){
  	document.getElementsByTagName("body")[0].style.backgroundColor=this.value;
  }
  ```

* date 日期

  ```html
  <input type="date">
  获取日期的时候使用的是value
  ```

* datetime  日期和时间

  ```
  只是一个输入框
  ```

* datetime-local 日期和时间不包括时区

* month 月份 显示年份和月份

* time 选择一个时间

* week 选择年和第几周

* email  用于输入e-mail

* tel 手机

* number 控制用户输入的区间   可以设置最大值和最小值 max="10"  min="0"  value="3"  step="2" step一次两格

* range 滑块

* search 搜索

* url 自动验证  只验证有内容的时候

* autocomplete="on/off"  是否让浏览器记住自己输入过的

* autofocus  自动获得焦点

* required  该属性用来验证，不允许内容为空，有空就提示并且不允许提交

* multiple   使用该属性允许用户上传多个文件

* pattern  使用方法pattern="正则表达式"，如果不符合规范会自动提示，并且不会提交





### 4.3 FileReader API

* API (Application Programming Interface,应用程序编程接口)是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问-组例程的能力，而又无需访问源码，或理解内部工作机制的细节。
* HTML5定义了FileReader对象作为文件API的重要成员用于读取文件，根据W3C的定义，FileReader接口提供了读取文件的方法和包含读取结果的事件模型。FileReader的 使用方式非常简单，创建FileReader 象并调用其方法即可
* FileReader的实例拥有4个方法，其中3个用以读取文件，另一个用来中断读取。下面的表格列出
  了这些方法以及他们的参数和功能，需要注意的是，无论读取成功或失败，方法并不会返回读取结
  果，这一结果存储在result属性中
  * readAsBinaryString           file                 将文件读取为二进制码
  * readAsDataURL                file                 将文件读取为DataURL
  * readAsText                        file                 将文件读取为文本   

**处理事件**
FileReader包含了一套完整的事件模型，用于捕获读取文件时的状态，下面这个表格归纳了这些事
件。文件一旦开始读取，无论成功或失败，实例的result属性都会被填充。如果读取失败，则result的值
为null，否则即是读取的结果，绝大多数的程序都会在成功读取文件的时候，抓取这个值。

* 事件							描述
  onabort						中断时触发
  onerror						出错时触发
  onload						文件读取成功完成时触发
  onloadend					读取完成触发，无论成功或失败
  onloadstart					读取开始时触发
  onprogress					读取中

this.files[0] 选取的是第一个文件

readAsDataURL读取文件的URL路径

result存储的是读取的结果，成功是结果，读取失败是null

onload文件读取成功完成后触发

```javascript
1.使用FileReader读取文件
document.getElementById("file").onchange=function(){
	var source=this.files[0];
	if(window.FileReader){//兼容性问题处理
		var fr=new FileReader();
		fr.readAsDataURL(source);
		fr.onload=function(e){
			e=e||window.event;
			document.getElementById("im").src=e.target.result;
			console.log("文件显示成功");
		}
	}
}
```









# CSS3

## 第一章 CSS3选择器

### 1.1 CSS3新特性

* 背景和边框
* 文字特效
* 2D/3D转换
* 动画
* 多列布局
* 用户界面

### 1.2 CSS3选择器

基本选择器：*、class、Id 、标记

关系选择器：包含、+、>、，

#### 属性选择器：

```css
E[attr]									    选取拥有此属性的E元素
E[attr="value"]								选取属性的值为value的E元素
E[attr^="value"]							选取属性的值为value开始的E元素
E[attr$="value"]							选取属性的值以value结束的E元素
E[attr*="value"]							选取属性的值含有value的E元素
E[attr~="value"]							选取多个属性值中包含value值的E元素
E[attr|="value"]							选择指定属性具有指定值开始的E元素。
```

```css
例1.
h1[name=h]/*name是属性 h是值 选取h1中name=h的项*/
	background-color:#f00;
}
```

#### 结构伪类选择器：

与jquery不同的是匹配父元素中的子元素是从1开始找的，而同类型且同级是从0开始找的

```css
所有的n都是从1开始的
以下是从所有的子元素中找
:root								根元素
E:empty								没有子元素的元素  空格也不可以
E:first-child						 父元素的第一个子元素E
E:last-child						 父元素的最后一个子元素E
E:nth-child(n)						 父元素的第n个子元素E
E:nth-last- child(n)				  父元素的倒数第n个子元素E
E:only-child						 父元素仅有的一个子元素E
以下找的是同级且同类型的
E:first-of- type					 同类型中的第一个同级兄弟元素E
E:last-of- type						 同类型中的最后一个同级兄弟元素E
E:only-of-type						 同类型中的唯一一个同级兄弟元素E
E:nth-of- type(n)					 同类型中的第n个同级兄弟元素E
E:nth-last-of-type(n)				  同类型中倒数第n个同级兄弟元素E
```

```css
:root{
	background-color:#f00;
}
div:last-of-type{
    background-color:#f00;
}
div:nth-of-type(1){
    background-color:#ff0;
}
```

#### 状态伪类选择器：

```css
:link				超链接访问前的样式
:visited			超链接被访问过后的样式
:hover				设置元素在其鼠标悬停时的样式
:active				设置元素在被用户激活时的样式
以下只有表单可以用
:focus				设置元素在成为焦点时的样式
:checked			匹配表单中，处于选中状态的元素E(用于type=radio|checkbox)
:enable				匹配表单E处于可用状态的元素E
:disabled			匹配表单上处于禁用状态的元素E
```

#### 伪类元素选择器：

```css
E:first-letter/E::first-letter		第一个字符
E:first-line/E::first-line			第一行
E:before/E::before				   对象前发生的内容，与content属性一起使用
E:after/E::after				   对象后发生的内容，与content属性 一起使用
```

```css
1.
h1::first-letter{第一个字符
	color:#f00;
}
2.
h1::before{
	content:"我是插入的内容";
	color:#f00;
}
```

### 1.3 content属性

* content一般和:before,:after一起使用，用来生成内容**(img和input没有该属性)**
* content的内容一般可以为以下四种(IE6-7不支持) :
  	--none:不生成任何值。
    	--attr:插入标签属性值
    	--url:使用指定的绝对或相对地址插入一个外部资源(图像，声频,视频或浏览器支持的其他任何资源)
    	--string:插入字符串

```css
1.
h1::after{写路径content
    content:url("img/1.jpg");
}
2.
h1::before{还可以在content中写属性会把属性的值获取出来放在h1前面
    content:attr(data-list);随意一个属性都可以使用attr
    color:#f00;
}
```

```css
需要注意的问题：
因为p:before或p:after选择器让所有p前面或后面插入文本，所以如果不想让指定p前面或者后面插入文本，那么可以使用content:none;
```

#### 插入项目符号

```css
语法：
1.
<元素>:before或after{
	content:counter(计数器);/*默认是阿拉伯数字*/
}
<元素>{
	content-increment:计数器;
}
2.
<元素>:before或after{/*浅白的表意数字 cjk-ideographic 就是一二三四*/
	content:counter(计数器,编号种类);/*编号种类是list-style-type属性值*/
}
<元素>{
	content-increment:计数器;
}
```

```css
1.
h1::before{
    content:counter(counter1);/*计数器的名字是自己写的*/
}
h1{
    counter-increment:counter1;/*写递增的计数器的名字*/
}
2.
h1::before{
    content:counter(counter1,cjk-ideographic);
}
h1{
    counter-increment:counter1;
}
```

#### 插入，和、号

```css
如果想要在后面加，或者、
h1::before{
    content:counter(counter1,cjk-ideographic)"、";直接在后面加就可以
}
h1{
    counter-increment:counter1;
}
```

加书名号、引号

```css
1.默认情况下是引号
h1::before{
    content:open-quote;
}
h1::after{
    content:close-quote;
}
2.书名号
h1::before{
    content:open-quote;
}
h1::after{
    content:close-quote;
}
h1{
    quotes:"<"">";第一个会用在open上面，第二个会用在close上面
}
```

#### 复位计数器

```css
h1::before{
    content:counter(counter1,cjk-ideographic);
}
h1{
    counter-increment:counter1;
    counter-reset:计数器
}
```

```html
<h1></h1>
<h2></h2>
<h3></h3>
```

```css
h1::before{
    content:counter(counter1)"、";
}
h1{
    counter-increment:counter1;
    counter-reset:counter2;/*在外层写里层的复位 给父元素加*/
}
h2::before{
    content:counter(counter1)"-"counter(counter2)"、";
}
h2{
    counter-increment:counter2;
    counter-reset:counter2;
}
h3::before{
    content:counter(counter1)"-"counter(counter2)"-"counter(counter3)"、";
}
h3{
    counter-increment:counter3;
    counter-reset:counter3;
}
```

### 1.4 CSS3属性的兼容问题

使用不同浏览器内核私有属性解决低版本浏览器对CSS3支持不好的问题

* -ms-	trident内核
* -moz-    gecko内核
* -webkit-    webkit内核
* -o-     presto内核

用法：

* -ms-border-radius:50%;
* -moz-border-radius:50%;
* -webkit-border-radius:50;
* -o-border-radius:50%;
* border-radius:50%;

## 第二章 新增样式（边框和背景）

### 2.1背景图片

#### background-size

```css
div{
    width:200px;
    height:200px;
    background-size:200px 200px;
    padding:20px
    background-img:url(../img/1.jpg);
    color:#0f0;
    border:1px solid #000;
}
```

#### background-clip  的原点一直都在左上角

* content-box 从内容开始  只有内容的显示
* padding-box 从padding开始
* border-box 从边框开始	默认

#### background-origin

与clip的区别就是clip的原点一致都在左上角，而Origin写哪个就从哪里开始

* content-box  
* border-box
* padding-box

### 2.2背景色渐变

#### 线性渐变

* background:linear-gradient(方向,颜色1，颜色2，颜色3)

  方向：to top |  to bottom  | to left | to right  还可以是对角的形式两个组合的方式to left top| to right top

  ```css
  background:linear-gradient(to top right,#f00,#0f0,#00f);对角
  background:linear-gradient(30deg,#f00,#0f0,#00f);30度
  ```


#### 径向渐变

```css
background:linear-gradient(#f00,#0f0,#00f,#ff0,#0ff);30度
```

#### 边框--圆角

* border-radius

  四个值：左上 右上 右下 左下

  三个值：左上角 右上角和左下角 右下角

  两个值：左上角和右下角 右上角和左下角

  一个值：4个角

#### 边界图片

* border-image:source slice width outset repeat;

  source:路径url();

  slice定义边界图片的切片，设置图像的边界向内的偏移长度

  width定义图像边框的宽度

  outset定义边框图像的偏移位置

  repeat定义边框展示方式stretch(拉伸，默认值)repeat(平铺)round(自动缩放图像进行平铺)

  ```css
  div{
  	width:500px;
      height:300px;
      border:#000 solid 70px;
      -webkit-border-image:url(../img/border.png) 70 round;有兼容性问题
  }
  ```

#### 阴影

* box-shadow用来给盒子模型添加阴影效果

  h-shadow必须，阴影的水平位置，允许负值

  v-shadow必须，阴影的垂直位置，允许负值

  blur 可选 模糊距离

  spread 可选 阴影的尺寸

  color 可选 阴影的颜色

  inset  可选 内阴影

  ```css
  div{
      width:150px;
      height:200px;
      background:#f00;
      box-shadow:20px 50px 10px 20px #aaa;
  }
  ```

## 第三章 CSS3文本效果和字体

* text-shadow 文字阴影

```css
p{
    text-shadow:10px 5px 5px #ccc;
}
第一个参数表示阴影的水平位置
第二个参数表示阴影的垂直位置
第三个参数表示阴影的模糊距离
第四个参数表示阴影的颜色
```

* 强制文本换行

  word-wrap:normal | break-word

  默认情况下单词或者是url地址都是在断点处换行，使用word-wrap:break-work；允许长单词或者是url地址换行到下一行，会从中剪短。

* 当文本溢出时发生的事

  text-overflow:clip | ellipsis;

  clip修剪文本，超出的部分隐藏

  ellipsis用省略号表示被修建的文本

* 注意：text-overflow属性要配合overflow:hidden一起使用才会生效

* 设置文本不进行换行

  white-space:nowrap

  nowrap:强制在同一行内显示所有文本，知道文本结束或者遭遇br对象

CSS3字体

```css
@font-face{
	font-family:name;/*此处名字可以自己起，但一定要跟引用font-family里面写的一致*/
	src:url(字体路径);
	font-weight:normal|bold;
}
```

## CSS3弹性盒子(flex box)

Flex是Flexible Box的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
任何一个容器都可以指定为Flex布局。
采用Flex布局的元素，称为Flex容器( flex container)，简称"容器"。它的所有子元素自动成为容器
成员，称为Flex项目(flex item)，简称"项目"。

#### Flex布局

容器默认存在两根轴:水平的主轴(main axis )和垂直的交叉轴(cross axis)。主轴的开始位置
(与边框的交叉点)叫做main start,结束位置叫做main end;交叉轴的开始位置叫做cross start,
结束位置叫做cross end。
项目默认沿主轴排列。单个项目占据的主轴空间叫做mainsize,占据的交叉轴空间叫做crosssize。

![image-20191225191723072](C:\Users\王加藤\AppData\Roaming\Typora\typora-user-images\image-20191225191723072.png)



* **任何一个容器都可以指定为Flex布局。**
  **display: flex;**
  **行内元素也可以使用Flex布局。**
  **display: inline-flex;**
  Webkit内核的浏览器，必须加上:-webkit- 前缀
  display: -webkit-flex; /* Safari */
  display: flex;

```html
<div>div1</div>
<div>div2</div>
<div>div3</div>
<div>div4</div>
```

```css
*{
    margin:0;
    padding:0;
}
div{
    background-color:#f00;
    height:200px;
    border:#fff solid 2px;
    display:inline-flex;
    display:-webkit-inline-flex;
}
```

#### 容器的属性

1. flex-direction 决定主轴的方向(即项目的排列方向)
row :默认值主轴为水平方向，起点在左端
row-reverse :主轴为水平方向，起点在右端
column:主轴为垂直方向，起点在上沿
column-reverse :主轴为垂直方向，起点在下沿

**父元素和子元素同时设置成弹性盒子,那么在显示的时候里面的子元素的宽度会由内容来决定,不管里面的子元素是否是块级元素**

**flex-direction的属性是给父元素添加的**

**flex-direction:colum就相当于没有使用flex盒子**

**使用flex-direction的时候,row:盒子宽度是由内容决定的,高度写多少是多少,column:盒子高度就是由内容来决定的**

```css
div{
    background-color:#000;
    height:200px;
    border:#fff solid 2px;
    font-size:40px;
    color:#fff;
    display:flex;
    display:-webkit-flex;
    display:-o-flex;
    display:-moz-flex;
    display:-ms-flex;
}
#outer{
    flex-direction:column;
    -webkit-flex-direction:column;
}
```

2. flex-wrap定义如果一条轴线排不 下，如何换行
    nowrap (默认)不换行
    wrap换行，第一行在上方
    wrap-reverse换行，第- -行在下方

```html
<div>
    <div class="inner">div1</div>
    <div class="inner">div2</div>
    <div class="inner">div3</div>
    <div class="inner">div4</div>
</div>
```

```css
div{
    background-color:#000;
    height:200px;
    width:500px;
    border:#fff solid 2px;
    font-size:40px;
    color:#fff;
    display:flex;
    display:-webkit-flex;
    display:-o-flex;
    display:-moz-flex;
    display:-ms-flex;
}
.inner{
    width:500px;
}
#outer{/*换行，不加就是不换行*/
    flex-wrap:wrap;
}
```

3. flex-flow该属性是flex-direction属性和flex-wrap属性的简写形式，默认值是row nowrap
   flex-flow : <flex-direction> || <flex-wrap>;

   ```css
   #outer{
       flex-flow:row-reverse nowrap;
       height:408px;
   }
   ```

4. **justify-content水平居中**
   flex-start(默认值)左对齐
   flex-end右对齐
   center居中
   space-between两端对齐，项目之间的间隔都相等

   space-around 每个项目两侧的间隔相等，所以项目之间的间隔比项目与边框的间隔大一倍

   ```css
   div{
       justify-content:center;/*水平居中*/
   }
   ```

5. **align-items垂直居中**
   flex-start垂直居上
   flex-end垂直居下
   center垂直居中
   baseline项目的第一行文字的基线对齐
   stretch(默认值)如果项目未设置高度或设为auto，将占满整个容器的高度。

   ```css
   div{
       align-items:center;/*垂直居中*/
   }
   ```

   让一个元素在页面上水平垂直居中

   ```css
   html,body{
       width:100%;/*必须宽高为100%*/
       height:100%;
   }
   body{
       display:flex;
       justify-content:center;
       align-items:center;
   }
   #d1{
   	width:300px;
       height:300px;
       background-color:#ff0;
   }
   ```

   子元素需要改变顺序或者方向的时候才需要给子元素设置为弹性盒子,否则只给父元素加就可以

#### 项目属性

1. order属性定义项目的排列顺序，数值越小，排列越靠前，默认值为0
    order :值 为数字可以是负数

  ```css
  .inner1{
      order:3;
  }
  .inner2{
      order:1;
  }
  .inner3{
      order:2;
  }
  .inner4{
      
  }
  ```

2. flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
    flex-grow : <number>
    如果所有项目的flex-grow属性都为1，则他们将等分剩余空间。如果一个项目的flex-grow属性为2,其他项目为1，则前者占据的剩余空间将比其他项目多一倍

  ```css
  div>div{
      flex-grow:1;/*平分*/
  }
  .inner1{
      order:3;
  }
  .inner2{
      order:1;
  }
  .inner3{
      order:2;
  }
  .inner4{
      flex-grow:2;/*分的就是剩余空间的两份*/
  }
  ```

3. align-self属性允许单个项目与其他项目不一样的对齐方式，可覆盖align-items属性，默认值为auto,**表示继承父元素的align-items属性，如果没有父元素，则等同于stretch**
    align-self : auto | flex-start | flex-end | center | baseline | stretch

**如果设置会覆盖align-items**



盒子模型 低版本box

注意：flex与box不允许混用

#### 盒子布局

1. 开启盒子布局
   display:-webkit-box;
   display:-moz-box;
   display:box;

2. 元素的布局方向--box-orient属性
   -webkit-box-orient: horizontal | vertical
      horizontal:设置弹性盒模型对象的子元素为水平排列
      vertical:设置弹性盒模型对象的子元素为垂直排列

   ```css
   #outer{
       height:400px;
       -webkit-box-orient:vertical;
       -webkit-box-direction:reverse;
   }
   ```

3. 元素的布局顺序-webkit-box-direction属性
   box-direction: normal | reverse
   normal:正常顺序排列
   reverse:反转排列顺序

4. 调整元素的位置-webkit-box-ordinal-group属性
   box-ordinal-group: <integer>
   <integer>:用整数值来定义弹性盒模型对象的子元素显示顺序

   ```css
   #outer{
       height:408px;
   }
   .inner{
       -webkit-box-ordinal-group:2;
   }
   ```

5. 弹性空间分配webkit-box-flex属性
   box-flex: <number>
   <number>:使用浮点数指定对象所分配其父元素剩余空间的比例

   ```css
   #outer{
       height:408px;
   }
   div>div{
       -webkit-box-flex:1;
   }
   .inner{
       -webkit-box-ordinal-group:2;
       -webkit-box-flex:2;
   }
   ```

   ```css
   自适应
   *{
       margin:0;
       padding:0;
   }
   #outer{
       height:200px;
       display:-webkit-flex;
   }
   .inner1{
       width:200px;
       height:100px;
       background-color:#f00;
   }
   .inner2{
       height:100%;
       bakcgroud-color:#0f0;
       flex-grow:1;
   }
   ```
   
6. 元素对其方式--box-pack和box- align属性
   box-pack: start | center| end| justify 水平
        start:左对齐
        center:居中
        end:右对齐
        justify:两端对齐
   box-align: start | end| center| baseline| stretch  垂直
        start:从开始位置对齐
        center:子元素居中对齐
        end:从结束位置对齐
        baseline:子元素基线对齐
        stretch:子元素自适应父元素尺寸

   ```css
   #outer{
   	height:408px;
       -webkit-box-pack:center;/*水平*/
       -webkit-box-align:center;/*垂直*/
   }
   ```


#### 增强的盒子模型

1. 盒子尺寸的计算方法--box-sizing属性
   box-sizing: content-box | border-box
      content-box: padding 和border不被包含在定义的width和height之内。
      border-box: padding 和border被包含在定义的width和height之内。
2. 溢出内容处理--overflow-x和overflow-y属性
   overflow-x: visible| hidden| scroll| auto
   overflow-y: visible| hidden | scroll| auto
      visible:不剪切内容。
      hidden:将 超出对象宽度的内容进行裁剪，将不出现滚动条。
      scroll:将超出对象宽度的内容进行裁剪，并以滚动条的方式显示超出的内容。
      auto: 在需要时剪切内容并添加滚动条，此为body对象和textarea的默认值。

## 多列布局

### display的取值

* none 隐藏对象。与visibility属性的hidden值不同，其不为被隐藏的对象保留其物理空间。
* inline 行内
* block 块
* list-item 列表项目
* inline-block 行内块
* table 作为块级的表格   **只有table的样式，没有table的特性**
* table-cell 列
* table-row 行
* flex 弹性盒子 新
* box 弹性盒子 旧

### 多列属性columns

1. columns:列宽，列数
2. 列间距：column-gap:值；列与列之间
3. 跨列：column-span：none/all   all是跨所有的列
4. 列分割线：column-rule：#000 solid 2px;
5. 鼠标类型：cursor：pointer/col-size；

### 用户界面设计

1. resize      resize：none/both/horizontal/vertical  可调整  必须要加上overflow:auto才起作用

```css
div{
    overflow:auto;
    width:200px;
    height:100px;
    resize:both;
    background-color:#f00;
}
```

2. outline  轮廓在边框外面，不包含有margin，不占用盒子模型。
3. 伪装元素  -webkit-appearance:button;
4. 倒影   box-reflect属性  -webkit-reflect:below;

## 第四章 2D和3D转换

#### 2D

1. transform属性 **有兼容性**

   transform:none;/transform-functions:设置一个或多个变形函数 

   1. 旋转rotate(x,y) xyz轴 可以单独写rotateX rotateY rotateZ

      transform:rotate(角度)  负数逆时针，以当前元素中心点旋转。

   2. 缩放scale(x,y)

      transform:scale(水平,垂直)  整数放大，小数缩小，0.5倍 scale(0.5,1)

      **可以复合写，transform:scale(0.5,1) rotate(60deg) 中间使用空格隔开**
   
   3. 移动translate(x,y)  
   
   4. 倾斜skew(x,y)
   
   5. 设置新的圆心 transform-origin:x,y   x取值left | center | right   y取值top | middle | bottom
   
      **不设置的情况下是以中间为圆心的。**

#### 3D变形

1. perspective  设置镜头到元素平面的距离即z轴到平面的距离，单位为px，离你越近就是正的，越远就是负的。***给body中设置**  开辟一个立体的空间

2. transform-style 是否让子元素保留3D效果

   取值：--flat:子元素将不保留其3D效果。

   ​		   --preserve-3d:子元素将保留其3D效果。

   旋转的时候，整个坐标系都会跟着动。z轴是相对于他本身。

## 第五章 CSS3动画

#### 5.1 过渡效果

* transition属性，有四个过渡属性（要谁过渡，过渡的时间[单位s]，过渡曲线，延迟时间）

  过渡曲线：linear匀速，ease-in慢开始，ease-out慢结束，ease-in-out慢开始慢结束

  例如：transition:width 2s，height 2s，background-color 2s;

  ```css
  div{
  	width: 200px;
  	height: 200px; 
  	background-color:#f00;
  	transform:rotate(0deg);
      transition: all 2s;
  }
  div:hover{
  	width:400px;
  	height:400px;
  	background-color:#ff0;
  	transform: rotate(360deg);
  }
  ```

  ```css
  /*鼠标滑入放大*/
  div{
  	width:136px;
  	height: 136px;
  	border: #000 solid 2px ;
  	overflow: hidden;
  }
  img{
  	width: 136px;
  	height: 136px; I
      transition:all 2s 1s;
  }
  img:hover{
  	transform:scale(1.5,1.5);
  }
  ```

  

#### CSS3动画

* 关键帧动画——@keyframes规则——创建动画   **有兼容性问题**

  语法：

  **fromto与百分比的区别是 fromto当回来的时候是没有过度的**

  ```css
  1. @keyframes name【动画名】{
      from{css样式}开始状态
      to{css样式}最终状态
  }
  2. @keyframes name【动画名】{
      0%{css样式}
      25%{css样式}
      50%{css样式}
      75%{css样式}
      100%{css样式}
  }
  ```

  ```css
  div{
      width:200px;
      height:200px;
      background-color:#f00;
  }
  div:hover{
      animation:all 2s forwards;
  }
  @keyframes anim{
      from{
          width:200px;
          height:200px;
          background-color:#f00;
      }
      to{
          width:400px;
          height:400px;
          background-color:#00f;
      }
  }
  ```

  ```css
  @keyframes anim{
      0%{
          background-color:#f00;
          transform:rotate(0deg);
      }
      50%{
          background-color:#0f0;
          transform:rotate(360deg);
      }
      100%{
          background-color:#00f;
          transform:rotate(720deg);
      }
  }
  ```

* 调用动画——animation(动画名，播放的时间) 【都为必填项】
  * 当动画完成后，是否保持最终状态forwards
  * 播放次数  默认1  循环播放infinite
  * direction  规定动画是否在下一周期逆向播放   reverse反向播放[只能用一次]   alternate奇数正向  偶数反向
  * delay  延迟的时间    单位是s或者ms

```css
/*滑入旋转360度，划出原路旋转回去*/
div{
    width:200px;
    height:200px;
    background-color:#f00;
}
@keyframes anim{
    0%{
        background-color:#f00;
        transform:rotate(0deg);
    }
    50%{
        background-color:#0f0;
        transform:rotate(360deg);
    }
    100%{
        background-color:#00f;
        transform:rotate(720deg);
    }
}
@keyframes anima{
    0%{
        background-color:#00f;
        transform:rotate(720deg);
    }
    50%{
        background-color:#0f0;
        transform:rotate(360deg);
    }
    100%{
        
        background-color:#f00;
        transform:rotate(0deg);
    }
}
```

```javascript
$(document).ready(function(){
    $("div").hover(function(){
        $(this).css("animation","anim 2s forwards");
    },function(){
        $(this).css("animation","anima 2s forwards");
    })
})
```

* 鼠标划入旋转

```css
img{
    width:150px;
    height:150px;
    border-radius:40px;
    border:#f00 solid 1px;
    transition:transform 2s;
}
img:hover{
    transform:rotateY(360deg);/*rotateZ,rotateX*/
}
```

* 鼠标滑入第一张图往上走，第二张图到第一张图的位置

```css
div{
    width:150px;
    height:150px;
    border-radius:40px;
    border:#f00 solid 1px;
    overflow:hidden;
}
img{
    width:150px;
    height:150px;
    transition:transform 1s;
}
```

```javascript
$(document).ready(function(){
    $("div").hover(function(){
  $(this).children("img").eq(0).css("transform","translateY(-150px)").next().css("transform","translateY(-150px)");
    },function(){
  $(this).children("img").eq(0).css("transform","translateY(0px)").next().css("transform","translateY(0px)");
    })
})
```

## CSS3响应式开发

* @media 媒介查询

  rem(单位)  根据根元素【html】的字体大小来改变的。

```css
宽度					320				384			480				640
屏幕对比比例			  0.5			  0.6		  0.75			   1
Html font-site		   10px    		    12px		15px			20px
元素宽度(px)		   100px			120px		150px			200px
元素宽度(rem)		   10rem			10rem		10rem			10rem
```

```css
@media only screen and(min-width:320px){
    html{
    font-size:20px;
	}
}
@media only screen and(min-width:480px){
    html{
    font-size:30px;
	}
}
@media only screen and(min-width:640px){
    html{
    font-size:40px;
	}
}
div{
    width:10rem;
    height:10rem;
    background-color:#f00;
}
```

* CSS3中的Media Query
  1. CSS3中的Media Query (媒介查询)是什么通过不同的媒介类型和条件定义样式表规则。媒介查询让CSS可以更精确作用于不同的媒介类型和同一媒介的不同条件。媒介查询的大部分媒介特性都接受min和max用于表达”大于或等于”和”小于或等于”。
  2. width 会有min-width和max-width媒介查询可以被用在CSS中的@media和@import规则上，也可以被用在HTML和XML中

* media query能够获取的值
  * **设备**的宽和高device-width，device-height显 示屏幕/触觉设备。
  * 渲染**窗口**的宽和高width，height显示屏幕/触觉设备。
  * 设备的手持方向，横向还是竖向orientation ( portraitlanscape)和打印机等。
  * 画面比例aspect-ratio点阵打印机等。
  * 设备比例device-aspect ratio-点阵打印机等。
  * 对象颜色或颜色列表color，color-index显 示屏幕。
  * 设备的分辨率resolution。

* 语法结构及用法
  * @media设备名only (选取条件) not (选取条件) and (设备选取条件)，设备二
    {sRules}
  * 字符间以空格相连，选取条件包含在小括号内，srules为兼容设置的样式表，包含在中括号
    里面。only (限定某种设备，可省略)，and (逻辑与)，not (排除某种设备)为逻辑关键字，
    多种设备用逗号分隔，这一点继承了css基本语法。
  * <link rel="stylesheet" type="text/css”media="only screen and (max-width:
    480px)，only screen and (max-device-width: 480px) ”href="link.css/>
  * 上面 使用中only可省略，限定于计算机显示器，第-一个条件max-width是指渲染界面最大
    宽度，第二个条件max-device-width是指设备最大宽度。
  * @media( min-device-width:1024px) and ( max-width:989px)，screen and ( max-
    device-width:480px)，( max-device-width:480px) and (orientation:landscape) ，
    (min-device -width:480px) and ( max-device-width:1024px) and
    (orientation:portrait) {srules}
  * 设置了电脑显示器分辨率(宽度)大于或等于1024px (并且最大可见宽度为989px) ;屏
    宽在480px及其以下手持设备;屏宽在480px以及横向(即480尺寸平行于地面)放置的手持设
    备;屏宽大于或等于480px小于1024px以及垂直放置设备的css样式。

* 使用Link设置响应式

  ```html
  <link rel="stylesheet" href="in.css" media="only screen and (min-width:720px),print and (min-width:450px)">
  <link rel="stylesheet" href="in2.css" media="only screen and (min-width:960px),print and (min-width:640px)">
  在哪个范围内就使用哪个css文件
  ```

媒介查询结合rem来实现

width、height、left、top、margin、padding









































































