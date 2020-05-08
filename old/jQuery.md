# 第一章 jQuery简介



jquery是Js的一个框架，没有属性，只有方法

为了简化原生JS，解决兼容性问题

主要用于PC端

Zepto用于移动端

## 1.1 JS的环境搭建

自己写的必须放在库的后面

```html
<script src="jquery.js" type="text/javascript"></script>
<script src="jq.js" type="text/javascript"></script>
```

```javascript
$(document).ready(function(){

}
$(function(){
	
})
```

## 1.2 JS的书写风格

不需要遍历，因为jQuery是隐式迭代

$代表的是jQuery

$(document).ready()表示在html加载完成之后在执行函数简写$()

```javascript
$(document).ready(function(){
	$("div").addClass("aa");
})

简写形式
这句话代表window.onload
$(function(){
	
})
```

## 1.3 js与jQuery之间的转换:

js:document.getElementsByTagName("div");

jquery:$("div");

# 第二章 生成jQuery对象

## 2.1 基本选择器

```javascript
#id				$("#test")
.class			$(".test")
标签		  	   $("p")
*				$("*")
匹配到的元素合并   $(#div,span,p.myClass)
```

## 2.2过滤选择器

### 2.2.1 基本过滤器(从0开始计数)

被隐藏的也可以被加上过滤器

```javascript
:first				选取第一个元素					    $("div:first")
:last				选取最后一个元素				   $("div:last")
:not()				选取所有与给定选择器不匹配的元素	  $("input:not(.myclass)")
:even				选取索引是偶数的所有元素			$("input:even")
:odd				选取索引是奇数的所有元素			$("input:odd")
:eq()				选取索引值等于index的元素从0开始		$("input:eq(1)")
:gt()				选取索引值大于index的元素从0开始		$("input:gt(1)")
:lt()				选取索引值小于index的元素从0开始		$("input:lt(1)")
:header				选取所有标题，如:h1,h2,h3,h4		$(":header")
:animated			选取当前正在执行动画的所有元素		   $("div:animated")
```

### 2.2.2 子元素过滤器(从1开始计数)

找的是所有孩子里面的，把所有的子元素都找到再找到匹配的，只能找儿子不能找孙子

```javascript
:nth-Child(index/even/odd/eq/表达式)		选取每个元素下的第index个子元素		$("p:nth-Child(3n+1)")
:first-Child							选取每个父元素的第一个子元素		    $("p:first-Child")
:last-Child								选取每个父元素的最后一个子元素		   $("p:last-Child")
:only-Child	如果某个元素是它父元素中唯一的元素将会被匹配，如果还有其他元素，则不会	  $("p:only-Child")
```

### 2.2.3 内容过滤器

```javascript
:contains()			选取含有符合括号中内容的元素				$("div:contains('hello')")
:empty				选取不包含后代元素和文本的空元素		$("div:empty") 选取不包含子元素的div的空元素
:has()				选取含有后代元素并匹配选择器的元素		  $("div:has(p)")选取含有P元素的div元素
:parent				选取有后代元素或文本的非空元素				$("div:parent")选取拥有子元素的div元素
```

### 2.2.4 可见性过滤器

```javascript
:hidden	选取的是内容和位置都隐藏的 type的值是hidden或display是none，其他的都不能被选中  visibility是hidden不能被选中
:visible		
```

### 2.2.5 属性过滤器

```javascript
[attribute属性名]			选取拥有此属性的元素				$("div[id]")
[attribute=value]		   选取属性的值为value				 $("div[id=top]")
[att!=value]
[att^=value]
[att$=value]			  选取属性值以value结尾的
[att*=value]			  选取属性值包含value的
[att~=value]			  选取多个
```

### 2.2.6层次选择器

```javascript
$("选择器1 选择器2")			后代
$("选择器1>选择器2")			子元素
$("选择器1+选择器2")			紧跟着的他的下一个兄弟
$("选择器1~选择器2")			后面所有兄弟 只要是选择器2的都能被选中
```

### 2.2.7表单对象元素过滤器

```javascript
:enabled	选取可用元素
:disabled	只要是不可用的都能被选中
:checked	单选多选：选取所有被选中的选项
:selected	下拉列表：选中所有被选中的选项
```

```
$(document).ready(function(){
	$(:checked+span).addClass("highlight");
})
```

### 2.2.8 表单选择器

```javascript
:input				选取所有的input、textarea、select、button
:text				选取所有的单行文本框
:password			选中所有的密码框
:radio				选取所有的单选框
:checkbox			选取所有的复选框
:submit				选取所有的提交按钮
:image				选取所有的图像按钮
:reset				选取所有的重置按钮
:button				选取所有的按钮
:file				选取所有的上传文件
:hidden				选取所有不可见元素
```

# 第三章 更改操作

1. 更改对象操作

   jQuery所作的事情就是生成jQuery对象，操作jQuery对象：像js一样如果对象之间存在某种关系我们就可以通过这种关联来改变对象，例如通过父元素找子元素

2. 链式操作设定

   

## 3.1 更改为后代的子元素

1.children()方法 选择子元素

children("选择器")选择子元素中，所有匹配选择器的子元素

children()/children("*")选择父元素的所有直接子元素

```
可以在children()括号里面写需要的元素
$("div").children("div").addClass("highlight")
```

2.find("选择器")方法 选择后代元素

find("选择器")选择后代元素中

3.contents()方法 选择文本块和子元素

```
选取原生元素中的子元素和文本块
$(function(){
    $("div[class^=top]").contents().addClass("highlight")
})
```

## 3.2更改为祖先元素集合

1.parent()找的是父元素

parent("选择器") 选择父元素中，所有匹配选择器的元素

parent()选择所有父元素

```
parent("选择器")选择父元素中，所有匹配选择器的元素
parent()选择所有父元素
```

2.parents()方法 选择祖先元素

parents("选择器")选择祖先元素中，所有匹配选择器的元素

parents()选择所有祖先元素

```
parents("选择器")选择祖先元素中，所有匹配选择器的元素
parents()选择所有祖先元素
```

3.parentsUntil()方法

parentsUntil("选择器") 选择祖先元素，直到找到匹配选择器的元素，但不包含匹配元素

parentsUntil() 选择所有祖先元素，与parents()功能一样

```
parentsUntil("选择器")选择祖先元素，直到找到匹配选择器的元素，但不包含匹配元素
parentUntil
```

4.offsetParent()方法

选择最近的祖先定位元素，且该元素的css属性display不能为none，所谓定位元素是指其css属性position取值为relative、absolute或fixed，如果祖先元素中没有合适的元素，则会选择body元素

括号里面不能写值 离他最近的有定位的

5.closest()方法 

选择本身或其祖先元素所匹配选择器的元素，也就是说先看该元素本身是否匹配，如果不匹配会一层一层向上找到最先匹配的祖先元素

找离他最近的祖先元素

## 3.3 更改为兄弟元素集合

1.next 下一个 prev 上一个

next()选择原先元素后面的第一个兄弟元素

next("选择器") 在原先元素后面的第一个兄弟元素中，选择匹配选择器的元素(不仅匹配后面的第一个兄弟)



prev("选择器")在原先元素前面的第一个兄弟元素中，选择匹配选择器的元素(仅匹配前面的第一个兄弟)

prev()选择原先元素前面的第一个兄弟元素

```javascript
$(document).ready(function(){
	$("div").next("h3").addClass("highlight");
})
```

```javascript
$(document).ready(function(){
	$("div").prev("h3").addClass("highlight");
})
```

2.nextAll()、prevAll()、siblings()方法

```javascript
nextAll():在原生元素后面的兄弟中，选取匹配括号中的元素 如果括号中为空会选取原生元素后面的所有元素
prevAll():在原生元素前面的兄弟中，选取匹配括号中的元素 如果括号中为空会选取原生元素前面的所有元素
siblings():	其他兄弟
```

```javascript
二级导航
$(document).ready(function(){
	$("#nav").children("li").mouseover(function(){
		$(this).children("ul").addClass("vi");
		$(this).siblings().children("ul").removeClass("vi");
	})
})
```

## 3.4 更改为更多元素集合

1.add()方法

```javascript
add("选择器")在原先元素的基础上添加选取匹配选择器的元素
$("选择器1").add("选择器2")等同于$("选择器1","选择器2")
```

2.andSelf()方法

```javascript
再更改对象之后，将原对象添加到选择的元素集合中
$("p").children("span").andSelf().addClass("highlight");
```

## 3.5更改为部分元素集合

1.eq()、first()、last()方法

```javascript
eq(index)选择元素中索引值等于Index的元素，正向从0开始，逆向从-1开始
first()选择匹配元素中第一个，等于eq(0);
last()选择匹配元素中最后一个，等于eq(-1);
```

2.slice()方法

```javascript
slice(start,[end-1])方法（不包含结束位置）
```

3.filter()和not()方法、has()

has后代元素

filter、not后面可以加方法

```javascript
fliter("选择器")在原先元素中选择匹配选择器的元素
not("选择器")在原先元素中选择不匹配选择器的元素
has("选择器")在原先元素中筛选出包含有括号中的后代元素的元素
```

```javascript
$("div").filter(".relative").addClass("highlight");
```

```javascript
找的是有P的div
$("div").has("p").addClass("highlight");
```

## 3.6 还原jquery方法

end()返回上一级 前提是必须要有上一级元素

```javascript
$("p").children("span").addClass("highlight").end().addClass("highlight");
```

```javascript
$("div").children("p").children("span").addClass("highlight").end().end().addClass("highlight");
```

## 3.7 链式操作：用一行代码完成多个效果

```javascript
$(document).ready(function(){
	$("#nav").children("li").mouseover(function(){
		$(this).children("ul").addClass("vi").end().Siblings().children("ul").removeClass("vi");
	})
})
```

# 第四章 文档处理

## 4.1 移动元素--没有就是添加

1.append()：向每个匹配的元素内部末尾追加内容。

```javascript
$("<p>p1</p>").appendTo($("div")).addClass("highlight");//把创建生成的p元素添加在每个div元素的内部尾端
```

```javascript
要添加到谁.append().需要添加的
$("div").append($("P")).addClass("highlight");
```

appendTo():将所有匹配的元素追加到指定的元素中

```javascript
$("div").append($("<p>p1</p>")).addClass("highlight");//把创建生成的p元素添加在每个div的内部尾端
$("div").append("<p>p1</p>").addClass("highlight");//同上
```

```javascript
需要添加的.appendTo("要添加到谁")
$("p").appendTo($("div")).addClass("highlight");
```

appendTo()和append()

```javascript
$("div").append(function(index,html){
	return html+"<p>p"+(index+1)+"</p>";
}).addClass("highlight");
//使用append方法把创建生成的不同p元素添加在每个div元素的内部尾端，其中index为div的索引值,html为div中原有的值，return中返回的是div中原有的值+（div的index值+1）
```

2.prepend():向匹配元素内部前面添加内容，有就移动，没有就添加

prependTo

```javascript
$("div").eq(0).prepend($("<p>p3</p>")).addClass("highlight");
```

```javascript
$("p").eq(0).prependTo($("div")).eq(0).addClass("highlight");
```

3.after():在每个匹配的元素之后插入内容

insertAfter():将所有匹配的元素插入到指定元素的后面

```javascript
$("p").eq(0).insertAfter($("div")).eq(0).addClass("highlight");
```

4.before():在每个匹配的元素之前插入内容

insertBefore():将所有匹配的元素插入到指定元素的前面

```javascript
$("div").before($("p")).addClass("highlight");//把p放到div前面,div高亮
```

```javascript
$("p").insertBefore($("div")).end().addClass("highlight");//把p放到div前面,p高亮显示
```

## 4.2 添加元素

1.复制元素

clone()包含子节点、文本和属性，默认

clone(true)会包含事件

```javascript
1.$("div").append($("p:first").clone()).addClass("highlight");//把复制第一个p元素生成的副本元素添加在每个div内部尾端
2.$("p:first").clone().appendTo($("div")).addClass("highlight");//把复制第一个p元素生成的副本元素添加在每个div元素的内部尾端
3.$("p:first").clone().appendTo($("div")).end().addClass("highlight");//把复制第一个p元素生成的副本元素添加在每个div元素的内部尾端,还原clone()方法对对象的更改，并给当前选定元素的class添加class
4.$("p:first").clone(true).appendTo($("div")).end().addClass("highlight");//把复制第一个p元素生成的副本元素添加在每个div元素的内部尾端,还原clone()方法对对象的更改，并给当前选定元素的class添加class,本次复制也会把P上面的事件复制过去
```

 2.替换元素

replaceWith()方法

先把需要替换的元素全部删掉，再把要替换的元素放在元素的后面，原先绑定在被删除元素上的事件已不复存在

```javascript
1.$("span").replaceWith($("p:first")).addClass("highlight");//使用replaceWith()方法删除全部span，同时把第一个P元素移动到最后一个span元素的位置
后面的把前面的替换掉
用后边的替换前边所有的，并且放到最后一个替换的元素位置
2.$("p").replaceWith($("span:lt(2)")).appendTo($("div:first")).addClass("highlight");//删除全部p元素，同时把前两个span移动到最后一个P元素的位置，使用appendTo方法把被删除的p元素重新放到第一个div元素的内部尾端，并给选定元素加上class
```

replaceAll()方法

```javascript
$("p").eq(0).replace($("span")).addClass("highlight");
前面的把后面的替换掉
用前面的替换后面的每一个，每一个都会被替换掉
1.$("p:first").replaceAll($("span")).addClass("highlight");//删除所有span，同时把第一个p元素移动到每个span的位置
2.$("p:first").replaceAll($("span")).end().addClass("highlight");//删除所有span,同时把第一个P元素移动到每个span的位置，给当前选定的元素加class
```

## 4.3 包裹元素

1.wrap()方法

 用wrap里面的元素把前面的元素包裹起来,在**包裹的时候是分别打包**的

```javascript
$("p").wrap($("div").eq(0)).addClass("highlight");
1.$("span:lt(2)").wrap($("p")).addClass("highlight");//复制全部P元素的第一个，用来包裹前两个span元素
```

2.解除包裹unwrap

删除原来的父元素，只剩里面的内容

```javascript
1.$("span:lt(2)").wrap($("p")).unwrap().addClass("highlight");//复制全部p里面的第一个，用来包裹前两个span元素，并且去除前两个span的父元素
```

3.warpAll()方法

把所有的元素包裹到一起

```javascript
$("p").wrapAll($("div").eq(0)).addClass("highlight");
1.$("span").wrapAll($("p")).unwrap().addClass("highlight");//复制全部p元素的第一个，用来把全部span元素包裹在一起
2.$("span").wrapAll($("p")).addClass("highlight");//复制全部p元素的第一个，用来把全部span元素包裹在一起
```

4.wrapInner()方法

会分别包裹每个元素内部的文本和后代元素，包裹里面的内容

先复制一个，再包裹

```javascript
$("div").wrap($("p"))  一个是把盒子包裹起来
$("div").wrapInner($("p"))  一个是把内容倒进去，再把盒子放进div里
$("span").wrapInner($("p")).eq(0).addClass("highlight");
1.$("span").wrapAll($("p")).addClass("highlight");//复制全部p元素的第一个，用来把全部span元素包裹在一起
2.$("div").wrapInner($("p")).addClass("highlight");//复制全部P元素中的第一个，用来包裹每个div元素内部
```

```javascript
//使用function生成不同的元素
$("div").wrapInner(function(index){
     return "<p>p"+(index+1)+"<p>";
}).addClass("highlight");//根据html字符串创建生成不同p元素
```



## 4.4 删除和清空元素

1.remove()方法可以删除当前，该元素所包含的**文本内容和后代元素以及事件同时被删除**

变量需要加$

```javascript
1.$("div>p:first").remove().addClass("highlight");//删除div元素内的第一个P元素
2.$("div>p:first").remove().appendTo($("div:first")).addClass("highlight");//删除div元素内的第一个P元素，使用appendTo方法把被删除的p元素移动到第一个div元素的内部尾端
3.例题：
$(document).ready(function(){
	$("div").eq(0).click(function(){
		alert("你单机了这个div1");
	})
	$("button").click(function(){
		var $d1=$("div").eq(0).remove();
		$("#d2").after($d1);
	})
})
```

2.detach()方法

删除当前元素，但是使用链式操作可以将删除的元素移动到其他位置，原先绑定在**内容位置删除事件会保留**

```javascript
$("div>p:first").detach().appendTo($("div:first")).addClass("highlight");//删除div元素内的第一个p元素，使用appendTo方法把被删除的p元素移动到第一个div元素的内部尾端
```

3.empty()方法

清空当前元素，该元素的文本内容以及所有后代元素都会被删除，**只删除内容，事件保留**

```javascript
$("div:first").empty().addClass("highlight");//清空第一个div元素
```

# 第五章 jquery对象的属性处理

## 5.1 元素的属性处理

1.attr()方法：获取元素的某个属性值，或者传递一个参数

```javascript
$("img").attr("width")不指定下标的情况下只能获取一个
$("img").attr("width","400")设置所有
```

```javascript
/*例题:加的值不固定的需要加function借助index*/
第一个参数获取的是索引值，第二个参数获取的是原来的值
$(document).ready(function(){
	$("button").click(function(){
		$("img").attr("title",function(index,value){
			return (index+1+value+)+".jpg";
		});
	})
})
```

2.removeAttr()方法:输出某个属性

```
$("img").removeAttr("width");
```

## 5.2 元素的class属性处理

1.使用attr添加class的方法

```javascript
$("img").attr("class","aa");
```

1.addClass()方法

attr设置属性值，先清空其他属性值，而addClass()方法可以在现有的基础上添加一个class

```javascript
$("img").addClass("aa");
```

2.removeClass()方法

不写值的情况下是全删，写值的情况下是指定

```javascript
$("img").removeClass();
```

3.toggleClass()方法

有这个class就删除，没有就给他加上

```javascript
$("button").eq(0).click(function(){
	$("img").toggleClass("aa");
})
```

```javascript
二级菜单
$("#nav").children("li").mouseover(function(){
	$(this).children("ul").toggleClass("vi").end().siblings().children("ul").removeClass("vi");
})
```

4.hasClass()

判断是否包含某个值，有返回true，没有返回false

```javascript
$("img").hasClass("aa");
```



## 5.3 元素内部的HTML、文本处理

1. Html()方法：相当于innerHTML

```javascript
$("div").html("我是一个div");
$("div").html(function(index){
    return "我是第"+(index+1)"个div";
})

```

2. text()方法：相当于innerText

```javascript
$("div").text(function(index){
    return "我是第"+(index+1)"个div";
})
//return "<p>我是第"+(index+1)"个div";
```



## 5.4 表单元素的属性处理

1. val()：获取或设置input匹配选择器的表单元素的value属性值

   ```javascript
   $("#username").blur(function(){
   	if($(this).val().length==0){
   		$(this).val("请输入用户名");
   	}
   })
   ```

   ```javascript
   $(document).ready(function(){
   	$("input").val(function(index){
   		return "我是第"+(index+1)+"个input";
   	})
   })
   ```

   隐式迭代：可以设置每一个，获取的时候获取第一个，都获取的时候手动遍历

2. 表单选项的checked、selected属性

# 第六章 jquery对css的处理

## 6.1 CSS基本属性的处理

1.css()方法

**可以设置复合属性，不能获取** 例如background、margin、border等，如果要获得Margin的值必须写margin-left、margin-top

```javascript
$("p").css("background-color");
$("p").css("backgroundColor");
$("p").css("background-color","#f00");
$("p").css({"background-color":"#f00","border-color":"#0f0","border":"1px solid #f0f"});//{属性:值，属性:值}可以设置复合属性，不能获取
//这种写法为json格式
```

## 6.2 CSS尺寸属性处理

1.height()和width()方法：如果要获取或设置CSS属性height、width的值，可以使用height()和width()

获取的值不一定是实际的宽高

```javascript
$("div").width();
$("div").eq(0).height("80%");百分比 设置所有div的width为父元素的70%
$("div").eq(0).height(80);像素
```

```javascript
$("div").eq(0).height($("div").eq(0).height()+30);
```

2.innerHeight和innerWidth()方法

获取的是实际高度和宽度，只能获取不能设置

```javascript
$("div").innerWidth();
```

3.outerHeight和outerWidth()方法

无法设置，默认不包含margin值，实际宽度+border+padding

```javascript
$("div").outerWidth(true);
```

## 6.3 CSS位置属性处理

1.offset()方法：获取或设置当前元素的相对窗口的偏移量

即使元素没有定位也可以给这个元素设置offset()

**设置的时候必须设置两个值top和left**

```javascript
$("div").eq(0).offset({"top":30,"left":40})//其实设置的就是top和Left的值，不管对象是谁，始终相对于窗口来说的
$("div").eq(1).offset().top
```

2.position()方法：获取离当前元素最近的有定位的祖先元素，**不能设置**

**父元素有定位到父元素，如果没有父元素会找body**

```javascript
$("p").position.top
```

3.scrollTop和scrollLeft()：**获取或设置滚动条滚的距离**

```javascript
$("p").eq(1).scrollTop(10)
```

```javascript
//function中的Index无论用不用都要写上因为第一个值代表的就是索引值
//例题：要想让top的值不变，让left的值改变
$("div").offset(function(index,coord){
	return {"top":coord.top,"left":20}
})
```



# 第七章 jquery对象的动画处理

## 7.1 隐藏与显示动画效果

1.hide()方法：动态改变当前匹配元素的高度、宽度和不透明度，最终隐藏当前元素，此使元素的属性display该为none

不写值的情况下默认是0.4秒  **改变的是宽高和不透明度**

```javascript
$("div").hide(2000);
$("div").show(2000);
```

2.show()方法：此元素的属性恢复为display为none

3.toggle()方法：隐藏的话就是显示，显示的话就是隐藏

```javascript
$("div").toggle(2000);
```

## 7.2淡入与淡出动画效果

1.fadeOut()淡出 隐藏 只改变透明度 **最终display的值为none**

```javascript
$("div").fadeOut(2000);
```

2.fadeIn()淡入 显示 最终display的值**为none以外的值**

```javascript
$("div").fadeIn(2000);
```

3.fadeToggle() 先把位置让出来 

```javascript
$("div").fadeToggle(2000);
```

4.fadeTo(时间，不透明度0-1)

```javascript
$("div").fadeTo(2000,0.5);只运行一次
```



## 7.3 滑入与滑出效果

1.slideUp() 改变当前元素的高度，最终为display:none

```javascript
$("div").slideUp(2000);
```

2.slideDown() 改变当前元素的高度 ，最终为非display:none

```javascript
$("div").slideDown(2000);
```

3.slideToggle() 隐藏的话就是显示，显示的话就是隐藏

```javascript
$("div").slideToggle(2000);
```



## 7.4 自定义动画效果

1.animate()方法：可以动态改变当前元素的各种css属性 **只有数值的才能改变 改变的是行内属性**

```javascript
$("div").animate({"left":"200px"},2000);
$("div").animate({"left":"200px","top":"200px"},2000);//同时变
$("div").animate({"left":"+=200px"},2000);
```



## 7.5 动画队列

 动画效果执行具有先后顺序，成为动画队列

```javascript
//先向右再向下
$("div").animate({"left":"200px"},2000).animate({"top":"200px"},2000);
```

### 7.5.1 延迟动画队列

delay()方法 delay(2000) 毫秒 

```javascript
$("div").animate({"left":"200px"},2000).delay(2000).animate({"top":"200px"},2000);
//谁需要就在谁后面加
```



### 7.5.2 中止动画队列

1.stop(**是否要清空未执行完**的动画队列，是否直接将正在执行的动画跳转到末状态)；两个参数均为true和false

```javascript
//如果两个参数都是false的情况下
$("div").animate({"left":"200px"},2000).delay(2000).animate({"top":"200px"},2000).animate({"left":"0px"},2000).animate({"top":"200px"},2000);
$("div").stop();
```

```javascript
//stop(true,flase)
$("div").animate({"left":"200px"},2000).delay(2000).animate({"top":"200px"},2000).animate({"left":"0px"},2000).animate({"top":"200px"},2000);
$("div").stop(true,false);
```

```javascript
//stop(false,true)
$("div").animate({"left":"200px"},2000).delay(2000).animate({"top":"200px"},2000).animate({"left":"0px"},2000).animate({"top":"200px"},2000);
$("div").stop(false,true);
```

```javascript
//stop(true,true)
$("div").animate({"left":"200px"},2000).delay(2000).animate({"top":"200px"},2000).animate({"left":"0px"},2000).animate({"top":"200px"},2000);
$("div").stop(true,true);
```

### 7.5.3 循环队列

在函数中封装起来，然后在函数内部调用一次，外面也调用一次

```javascript
function loop(){
$("div").animate({"left":"200px"},500).animate({"top":"200px"},500).animate({"left":"0px"},500).animate({"top":"0px"},500)
    loop()
}
$("div").click(function(){
    loop();
})
$("button").click(function(){
    $("div").stop(true,false);
})

```

## 7.6 动画回调函数

当这个动画执行完成后再执行这个function

```javascript
//先右移再变色
$(document).ready(function(){
	$("div").click(function(){
        $(this).animate({"left":"200px"},1000,function(){//直接在时间后面写,function(){}
            $(this).css("background-color","#ff0");
        });
    })
})	
```

# 第八章 jQuery对象的事件处理

## 8.1 window.onload和$(document).ready(function(){ })区别

1. window.onload不能简写

2. window.onload只能执行一次 从上往下而$document是执行多次

3. window.onload所有加载完了 他才会加载

   $document 相应的document加载完了 他也会加载完成

## 8.2 绑定事件——bind()方法

mouseover与mouseenter区别：动一次就会触发Over 在上面的时候就不会触发enter 出来的时候触发一次

### 1.bind("事件名称","处理函数")

常用的事件有:click、dbclick、mouseup、mousedown、mouseenter、mouseleave、mouseover、mouseout、focus、blur、focusin、keyup、keydown、keypress、change、select、submit、load、unload、resize、scroll、error等

bind只能给html原有的绑定事件，新添加的一个元素是不能有事件的

```javascript
$(document).ready(function(){
	$("div").bind("mouseenter",function(){
		$(this).html("你操作了这个div");
	})
})
```

**如果想绑定多个事件在事件之间加空格 前提是这两个事件同时调用的是一个处理函数**

```javascript
$(document).ready(function(){
	$("div").bind("mouseenter mouseleave",function(){
		$(this).html("你操作了这个div");
	})
})
```

**同样的事件 绑定多少个就执行多少次**

### 2. 解除绑定 unbind("事件名称","处理函数")

**用什么事件绑定就得用对应的解除绑定解除**

```javascript
$(document).ready(function(){
	$("div").bind("click mouseenter",function(){
		$(this).html("你单机了这个div");
	})
	$("button").click(function(){
		$("div").unbind("click");
	})
})
```



## 8.3 绑定事件——one()方法

one()就执行一次 自动解绑

```javascript
$(document).ready(function(){
	$("div").one("click",function(){
		$(this).append("<p>你单机了这个div</p>")
	})
})
```

## 8.4 绑定事件——on()方法

用on()进行绑定，用off进行解除

```javascript
$(document).ready(function(){
	$("div").on("click",function(){
		$(this).append("<p>你单机了这个div</p>")
	})
	$("button").off()
})
```

如果绑定多个事件，不需要写多个on直接采取on{}在里面事件名:function 每个事件用，隔开

```javascript
$("div").on({
	mouseenter:function(){
		$(this).html("你划入了这个div");
	},
	mouseleave:function(){
		$(this).html("你画出了这个div");
	}
})
```

on()可以在绑定事件的同时传数据，直接使用的是对象的方式来表示的，{属性：值，属性：值}，这个值是字符串直接加引号，是数值直接写

获取的时候直接是e.data.属性名获取即可，e代表的是事件对象，data代表的是事件对象上面存数据的

类型可以是对象，字符串，数组

```javascript
//此处的e没有兼容性
$("div").on("click",{name:"Lily",age:19,sex:"女"},function(e){//书写的时候大括号,属性名:""使用,隔开
	alert(e.data.age);
})
//在获取相应的属性的时候用事件e.data.属性age
```

## 8.4.1 on触发事件——自定义事件 

事件名：function(){}

trigger(事件名)  刷新时自动触发一次

```javascript
$("div").live("myEvent",function(){
	alter("你单机了这个div");//此处写什么触发的时候就出什么
})
$("div").trigger("myEvent");
```

## 8.4.2 触发事件——命名空间

触发click事件及命名空间aa 命名空间里面的click事件

在事件后面.命名空间(小名) click.aa

想要触发不是命名空间的这个在事件click!

```javascript
$(document).ready(function(){
    $("p").bind("click",function(){
        $(this).append("<span>1、发生了鼠标单击事件</span>");
    })
    $("p").bind("click.aa",function(){
        $(this).append("<span>2、发生了鼠标单击事件</span>");
    })

$("#btn1").click(function(){
    $("p").trigger("click");//触发click事件及命名空间aa里面的click事件
})
$("#btn2").click(function(){
    $("p").trigger("click.aa");//只触发命名空间aa里面的click
})
$("#btn3").click(function(){
    $("p").trigger("click!");//只触发不在命名空间aa里面的click
})
});
```

## 8.4.3 触发事件——触发事件时传递数组数据

数据在当前处理函数的参数中，与data无关

第一个参数为事件对象参数，之后的参数为传的数据

传值在触发的时候传值 使用数组的方式

```javascript
1.function(e,value1,value2){
	
}
2.$("div").bind("click",function(e,param1,param2){
    $(this).html(param1+param2);
})
$("div").trigger("click",["第一个值","第二个值"]);//trigger自动会触发一次
```

## 8.5 委派事件——live()方法

只能给html原有的绑定事件，新添加的一个元素是不能有事件的，为了解决这个问题使用live()方法

```javascript
$("div").live("click",function(){
	$(this).html("你单机了这个div");
})
$("body").append("<div></div>");
```

## 8.5 移除委派事件——die()方法

```javascript
$("div").live("click",function(){
	$(this).html("你单机了这个div");
})
$("body").append("<div></div>");
$("button").click(functon(){
	$("div").die();//移除委派在div上的所有事件
})
```

## bind与on的区别

* bind：如果想绑定多个事件在事件之间加空格 前提是这两个事件同时调用的是一个处理函数
* on:可以同时绑定多个不同事件 有多少个就写多少个function(){} 用逗号隔开

## bind、live、one、on的区别

* bind:正常绑定，绑定几个执行几个，不能给新添加的元素进行绑定
* live:可以给新添加的元素进行绑定上指定的事件
* one:只执行一次，执行完成之后自动解除绑定
* on:可以同时绑定多个不同事件处理函数的时间{事件名：function(){}，事件名：function(){}}

## 8.6 事件类型

1.**鼠标点击事件**

* click事件——单击
* dbclick事件——双击
* mousedown事件——鼠标按下
* mouseup事件——鼠标抬起

2.**鼠标移动事件**

* mouseenter——鼠标指针进入某个元素事件
* mouseleave——鼠标离开某个元素
* mouseover——鼠标指针进入某个元素或其后代元素
* mouseout——鼠标指针离开某个元素或其后代元素
* mousemove——当鼠标在某个元素或其后代元素移动

3.**得到焦点和失去焦点**

* focus事件——通过鼠标单击或Tab键定位元素触发

* blur事件——元素失去焦点事件

* focusin事件——通过单击或Tab键定位元素或元素的后代元素获得焦点

* focusout事件——通过鼠标单击或Tab键定位元素的后代元素失去焦点

  ```javascript
  $("div").focusin(funciton(){
  	$(this).append("<span>input获得了焦点</span>");
  })
  ```

4.**键盘事件**

* keydown事件——按下键盘上的任意键，会触发获得焦点元素的keydown事件
* keyup事件——按下键盘上的任意键，会触发获得焦点元素的keyup事件
* keypress事件——当想获得焦点的元素输入一个字符时，会触发该元素及其祖先元素发送的keypress

5.**表单事件**

* change事件——当表单元素的value属性值或选中项发生变化时，会触发该属性及其祖先元素发送的change事件

* select事件——当在input或textarea元素内进行文本选中时，会向该元素及其祖先元素发送select事件。需要注意，在IE浏览器中并不会向触发元素的祖先元素发送select事件

* submit事件——通过Input type=submit，input type=image或button type=submit元素或当其获得焦点时按下回车，可以提交表单

  ```javascript
  $(document).ready(function(){
  	$("input").select(function(){
  		alert("你选中了这个input元素的内容")
  	})
  })
  ```

6.**加载和卸载事件**

* load事件——当某个元素及其后代元素已经完全加载时
* unload事件——当离开当前页面时

### 8.6.1 事件类型——合成事件

1. hover()方法：合成的是mouseenter和mouseleave

hover(处理函数1()，处理函数2())

```javascript
$("div").hover(function(){
	$(this).html("你划入了这个div");
},function(){
	$(this).html("你画出了这个div");
})
```

2. toggle()方法：单击的合成事件

第一个处理函数表示第一次单击，第二个处理函数表示第二次单击，如此下去，如果处理函数为2单击第三次的时候返回第一次执行

```javascript
1.$("div").toggle(function(){
    $(this).html("你单机了1次");
},function(){
    $(this).html("你单机了2次");
},function(){
    $(this).html("你单机了3次");
})
2.$("button").toggle(function(){
	$("div").fadeIn(1000);
},function(){
	$("div").fadeOut(1000);
})
```



jquery表单验证，jquery实现返回顶部，阿里效果，二级导航使用hover，toggle一点击会出来再点击消失（动画）



## 8.7 事件对象

事件对象是一个事件发生时，保存事件各个相关信息的对象，在程序中使用事件对象非常简单，只需腰围事件处理函数添加一个event（e）参数即可

### 8.7.1 阻止默认行为的方法

e.preventDefalut()

```javascript
$("a").click(function(e){
	e.preventDefalut();
	$(this).next().html("你阻止了a的跳转");
})
```

### 8.7.2 阻止事件冒泡的方法

1.e.stopPropagation()		注意大写P

2.return false      		后面的都不执行

3.triggerHandler()	   

```javascript
1.$("div").click(function(e){
	e.stopPropagation();
	alert("你单机了div");
})
```

```javascript
2.$("div").click(function(e){
	alert("你单机了div");
	return false	//return false
})
```

```javascript
3.$("div").click(function(e){
	alert("你单机了div");
})
$("#d3").triggerHandler("click");
//在triggerHandler()括号里要指定事件，不管是否有多个事件都需要指定
```

拖拽

```javascript
//拖拽改变大小原理：
1.需要判断鼠标有没有按下,isDown就是用来判断鼠标按下,true
2.再mousedown直接后才是true，up之后就是false
3.mousemove，move就需要判断true，获取宽度，宽度就是e.offset:左边元素的宽度，右边元素的宽度，总的-offsetX
```

```css
p{float:left;text-align:center;line-height:100px;margin:0;}
#zt{width:1300px;height:500px;border:1px solid #000;}
#left{width:1199px;height:500px;background-color:#963;}
#right{width:99px;height:500px;background-color:#ff0;}
#hr{width:2px;height:500px;background-color:#f00;border:0;cursor:col-resize;}
```

```html
<div id="zt">
	<p id="left">左边</p>
	<p id="hr"></p>
	<p id="right">右边</p>
</div>
```

```javascript
var l=document.getElementById("left");
var r=document.getElementById("right");
var h=document.getElementById("hr");
var z=document.getElementById("zt");
var isDown;
z.onmousedown=function(){
    isDown=true;
}
z.onmouseup=function(){
    isDown=false;
}
z.onmousemove=function(e){
    e=window.event || e;
    if(isDown){
        var hx=e.clientX;
        if(hx<1199&&hx>99){
            l.style.width=hx+"px";
            r.style.width=(1298-hx)+"px";
        }
    }
}
```



## 8.10 事件对象传递参数

事件对象传递参数：当调用bind()或one()方法为元素绑定事件时，还可以选用参数data来传递额外的信息，并利用事件对象的data属性在时间处理函数中进行接收，通常这个参数可以解决由于事件处理函数使用外部变量造成的问题

```javascript
1.
var message="data1";
$("p:eq(0)").bind("click",function(){
	$(this).text("变量message的值为"+message);
});
var message="data2";
$("p:eq(1)").bind("click",function(){
	$(this).text("变量message的值为"+message);
});//变量message的值为data2，变量message的值为data2
//为两个p元素分别绑定click事件，当鼠标单击某个元素时，会修改其文本的内容，在这个事件处理函数里面，外部变量Message的值均为data2  由此可见，事件处理函数只能使用外部变量的最终值，而无法获得外部变量的当前值。



2.$(document).ready(function(){
    $("div").bind("click",{"name":"Lily","age":19},function(e){
        console.log(e.data);//输出的为{name: "Lily", age: 19}  e.data就是里面的数据
    })
})

3.$(document).ready(function(){
    $("div").bind("click",{"name":"Lily","age":19,"talk":function(str){
        {alert(str)}
    }},function(e){
        // console.log(e.data);
        // console.log(e.data.age);
        // e.data.talk(e.data.name);
    })
})
```

## jQuery this指向问题

```javascript
$(document).ready(function(){
	$("div").animate({"widht":"400px"},1000,function(){
		$that=$(this);//给他赋值给一个变量这个that指向的是div
		$("p").animate({"width":"200px"},1000,function(){
			$that//这个that指向的是div
		})
	})
})
```

## 8.11 事件对象的触发键

如果需要知道触发事件的案件，那么可以使用事件对象的which属性，在鼠标点击事件中,which属性

1表示左键 2表示中键 3表示右键

which的键盘按键值：查看ASCII表

## 8.12 事件对象的发生位置和发生的时间

如果要跟踪事件触发时的鼠标位置，那么可以使用pageX和pageY属性，这两个属性分别提供了鼠标指针位置相对于页面左上角的x坐标和y坐标

```javascript
例：
$("p").mousemove(function(){
	$("p:eq(0)").text("移动鼠标相对于页面的坐标："+event.pageX+","+event.pageY);
})
```

如果需要跟踪事件发生的时间，那么可以使用事件对象的timeStamp属性，这个属性能够返回事件触发时距离1970年1月1日的毫秒数

## jquery：内置对象、BOM、自定义对象

# 第九章 jquery对象的对其他元素的处理

## 9.1 对元素进行遍历操作

如果要遍历一个对象，要对其中每个匹配的元素进行遍历，使用each()方法

显示迭代

```javascript
对象.each(function(){

})
//可以根据索引值Index进行判断
$("div").each(functon(index){
	if(index==2 || index>5){
    	$(this).css({"background-color":"#0ff"});
}
})
```

## 9.2 对元素进行数据存取

在元素上存储数据，将数据存储在元素data方法的参数中

```javascript
语法：
data("变量名"，值)
1.$(document).ready(function(){
    $("div").data("test","好好学习天天向上！！！");
    console.log($("div").data("test"))
})
2.$(document).ready(function(){
    var msg="Hello";//使用变量
    $("div").data("test",msg);
    console.log($("div").data("test"))
})
3.$(document).ready(function(){
    var msg="Hello";
    $("div").data("test",{"name":"Lily","age":19});
    console.log($("div").data("test").name);
})
4.$(document).ready(function(){
    var person=[1,2,3,4,5];
    $("div").data("test",person);
    console.log($("div").data("test")[0])
})
```

## 9.3 清除附加在元素上的变量

removeDate()方法

语法removeDate(name)

删除指定参数名的数据，如果要清除元素上的全部变量使用removeDate()不带参数

```javascript
$(document).ready(function(){
    $("div").data("test",{"age":19})
    $("div").removeData();
    console.log($("div").data("test"));
})
```

## 9.4 元素的个数

1.size()方法:计算jquery对象中元素的个数

```javascript
$("p").size()//4
//说明：通过jquery对象的Length属性，也能得到JQuery对象中元素的个数
$("p").length;//4


//可以判断JQuery对象是否为空
if($("span").length==0){
    alert("不存在span元素");
}
```

## 9.5 元素的索引

index找的是相对于所有兄弟的索引值

```javascript
$("#d3").index();//返回从0开始的索引值 如果不指定所有标记都计算在内
```



鼠标划入图片跟随鼠标放大

```javascript
$(document).ready(function(){
	var offsetX=20-$("div").offset().left;//
	var offsetY=20-$("div").offset().top;//
	var size=2*$("img").width();//按照原来的图片放大二倍
	$("div").mouseover(function(event){
		var $target=$(event.target);//target返回触发当前事件的对象
        if($target.is("img")){
            $("<img id='tip' src='"+$target.attr("src")+"'>").css({
                "width":size,
                "height":size,
                "left":event.pageX+offsetX,
                "top":event.pageY+offsetY
            }).appendTo($("div"));
        }
	}).mouseout(function(){
        $("#tip").remove();
    }).mousemove(function(event){
        $("#tip").css({
            "left":event.pageX+offsetY,
            "top":event.pageY+offsetY
        })
    })
})
```

淘宝小方块拖动放大镜

```javascript
$(document).ready(function(){
	$("#left").children("img").mousemove(function(event){
		var $left=event.pageX;
		var $top=event.pageY;
		var $sizeLeft=3*event.pageX;
		var $sizeTop=3*event.pageY;
		$(this).next("span").css({"left":$left,"top":$top})
		$("#right").children("img").css({"left":-$sizeLeft,"top":-$sizeTop});
	})
})
```

# 第十章 jquery的基本方法

插件与方法的区别

```javascript
对象.each()//方法
$.each(对象.function(){//插件

})
$.函数名(要操作的对象)插件
```

## 10.1 处理字符串的方法

1.去除字符串中两端空格$.trim(str)  中间的空格去除不掉

```javascript
var str="   好好学习，天天向上！！！  "：
alert(str);
alert($.trim(str));
```

## 10.2处理对象的方法

遍历对象的数据并进行操作$.each(对象，function(属性名【数组的话为索引值】，value【每一项的内容】))

这里遍历的对象为Json对象和array对象

```javascript
var arr=[5,6,7,8,9,0];
var obj={"name":"Tom","sex":"man","age":20};
$.each(obj,function(index,value){
	console.log(index+","+value);
})
```

## 10.3 处理数组的方法

对数组中数据项进行筛选，返回一个新数组$.grep(arr，fn(n，i))，不能操作对象

n，j分别表示数组值和索引

```javascript
var arr=[5,6,7,8,9,0];
var arrNew=$.grep(arr,function(value,index){
	return value>6&&index<4//数组项大于6并且索引值小于4
})
	console.log(arrNew);
```

## 10.3 处理数组的方法$.map(arr，fn(n,j))

要对**数组**中的数据项进行修改、删除、添加，来获得一个新的数组$.map(arr，fn(n,j))

```javascript
var arr=[5,6,7,8,9,0];
var arrNew=$.map(arr,function(value,index){
	return (value+index)//索引值加数组项
    return [index,value] //索引值增进去
    return index>3?value?null;//如果索引大于3就返回里面的值，否则删除
})
	console.log(arrNew);
```

```javascript
$(document).ready(function(){
	var obj=[{"name":"韩梅梅","sex":"女","age":20},{"name":"喜羊羊","sex":"男","age":20},{"name":"光头强","sex":"女","age":40}];
	$.map(obj,function(value,index){
		$("body").append("<div><h3>"+value.name+"</h3><p>"+value.sex+"</p><p>"+value.age+"</p></div>")
	})
})
```

## 10.4 $.merge(arr1,arr2)

把两个数组中的数据项合并在一个，来获得一个新数组，$.merge(arr1,arr2)，参数arr

```javascript
var arr1=[1,3,4];//arr1这个数组会变，arr2不变
var arr2=[2,3,4];
var arrNew=$.merge(arr1,arr2);
console.log(arr1);
console.log(arr2);
console.log(arrNew);
```

## 10.5 处理数组的方法$.inArray

检索数组，有返回下标，没有返回-1

```javascript
$.inArray(value,arr)//格式
var arr1=[1,2,3];
console.log($.inArray(4,arr1));
```

# 第十一章 AJAX











# 第十二章 jQuery插件

## 12.1 jQuery插件

```javascript
each:对象.each(function(){}),$.each(对象,function(){})
```

* 创建插件的方法分为两种
* 第一种是对jQuery方法进行扩展的，$.方法名(参数，参数) $.方法名(参数，参数)
* 第二种创建插件的方法：扩展的是jQuery对象的方法，对象.方法名(function(){})

js有封装--jquery插件

## 12.2 第一类插件，扩展jquery的方法

```javascript
$.funName=function([参数1，参数2]){代码块}
$.funName({参数1，参数2，参数3});
```

```javascript
$(document).ready(function(){
	var arr1=[2,345,56,9,8];
	var arr2=[3,2,4,5,7];
	var arrNeW=[];
	$.each(arr1,function(index,item)){
		//arrNew[index]=max(item,arr2[index]);js写法
           arrNew[index]=$.max(item,arr2[index]);
	}
})
//max=function(a,b){javascript写法
	//if(a>b){
		//return a;
	//}else{
		//return b;
	//}
//}
$.max=function(a,b){//jquery写法
	if(a>b){
		return a;
	}else{
		return b;
	}
}
```

## 12.3 第一类插件另一种构造方法，通过$.extend()方法  封装多个插件

```javascript
$.extend({
	插件名:function(参数1，参数2){}，
	插件名:function(参数1，参数2){}，
})
```

```javascript
$(docuemnt).ready(function(){
    $.navSlide($("#nav").children("ul").children("li"),"ul");//这里的第二个值之所以是ul因为在children里面直接写的就是"ul";
})
$.extend({
	max:function(a,b){
		return a>b?a:b;
	},
	min:function(a,b){
		return a>b?b:a;
	}
    navSlide:function(a,b){
    	a.hover(function(){
            $(this).children(b).slideDown(1000);
        },function(){
            $(this).children(b).slideUp(1000);
        })
	}
})
$.max(item,arr2[index])//
$.min(item,arr2[index])
```



作业：表单验证 返回顶部 无缝滚动 二级导航

作业：图片放大缩小，选项卡

## 12.4 构造第二类Jquery插件

这种方法，有要操作的对象，可以直接给这个对象加样式  

$.fn.插件名=function([参数1，参数2]){}--->创建方法

$(obj).插件名()--->调用方法  

```javascript
1.$(docuemnt).ready(function(){
    $("#nav").children("ul").children("li").navSlide("ul");//$(要操作的对象).插件名()
})
$.fn.navSlide=function(b){//单独使用
    $(this).hover(function(){
        $(this).children(b).slideDown(1000);
    },function(){
        $(this).children(b).slideUp(1000);
    })
}
```

* 创建多个的时候还是使用extend

在Jquery中extend这个方法专门用来创建插件的，在extend中写的时候需要遵循对象的写法{插件名:function(){},插件名:function(){}}

调用的时候，用的是哪种方法创建插件的，就是用哪种方法进行调用

但是一般情况下我们在使用的使用扩展对象的方法是最多的，$.fn.funName=function(){}，因为在这个方法中有操作对象，想要当前的操作对象进行其他操作的话可以直接找到这个对象。就是在调用完了插件之后，继续进行其他的操作

将封装的文件

顺序：先引入jquery文件--然后封装文件---本身jquery代码

```javascript
2.$(docuemnt).ready(function(){
    $("#nav").children("ul").children("li").navSlide("ul");//$(要操作的对象).插件名()
})
$.fn.extend({
    navSlide:function(b){
        $(this).hover(function(){
            $(this).children(b).slideDown(1000);
        },function(){
            $(this).children(b).slideUp(1000);
        })
    }
})
```

对象.each()-->对数组进行遍历的，它操作的是每一个需要遍历的对象，所以如果想要返回去操作这个数组对象的话，那么需要加上return 

```javascript
$(docuemnt).ready(function(){
    $("#img").big().css({"border":"1px solid #000"})//$(要操作的对象).插件名()
})
$.fn.extend({
    big:function(){
        return $(this).hover(function(){//让他返回最一开始的对象给他加上样式
            $(this).animate({"width":"200px","height":"200px"},1000)
        },function(){
            $(this).animate({"width":"100px","height":"100px"},1000)
        })
    }
})
```

## 12.5 优化Jquery插件设置传入参数的默认值

设置传入参数的默认值

```javascript
$(docuemnt).ready(function(){
    $("#nav").children("ul").children("li").navSlide("ul");//$(要操作的对象).插件名()
})
$.fn.extend({
    navSlide:function(b){
        if(b==undefined){//需要注意的点：undefined不能用引号引起来
            b="ul";//默认为ul
        }
        $(this).hover(function(){
            $(this).children(b).slideDown(1000);
        },function(){
            $(this).children(b).slideUp(1000);
        })
    }
})

//需要注意的点：undefined不能用引号引起来
if(b==undefined){
    b="ul";
}
```

## 12.6 优化jquery插件 隐藏私有的函数和变量

```javascript
(function($){
	jquery插件方法
})(jQuery)或($)
jquery插件调用
```

```javascript
$(docuemnt).ready(function(){
    $("#nav").children("ul").children("li").navSlide("ul");//$(要操作的对象).插件名()
})
$.fn.extend({
    navSlide:function(b){
        if(b==undefined){//需要注意的点：undefined不能用引号引起来
            b="ul";//默认为ul
        }
        $(this).hover(function(){
            $(this).children(b).slideDown(1000);
        },function(){
            $(this).children(b).slideUp(1000);
        })
    }
})(jQuery)
```

在js中创建变量使用的var进行创建的，创建出来之后就是一个全局变量，使用var创建出来的变量可以进行变量提升，在提升的时候会把当前变量提升成为全局变量，之后如果在需要使用的话就会污染当前这个全局变量，为了避免污染所以需要把这些方法放在匿名函数中进行调用。

es5中只有一种创建变量的方式就是var 

es6中新增了两种

所以我们在创建插件的时候把创建插件的方法全都放在匿名函数中，作为私有函数和变量进行使用。





# Firebug

* 针对火狐的插件，可以通过设置断点进行查看 ，可以对网络进行查看和监听，可以再控制台中写Js 提供的是js环境

## 1.1控制台——显示信息的命令

```javascript
console.info("这是info");一般信息
console.debug("这是debug");出错信息
console.warn("这是warn");警告提示
console.error("这是error");错误提示
```

## 1.2控制台——占位符

%s字符，%d或者%i整数，%f浮点数，%o对象

```javascript
console.log("%d年%d月%日",2011,11,26);
console.log("姓名:%s","张三");
```

```javascript
var person={};
person.name="Lily";
person.age=20;
console.log("这是一个对象：%o",person);
```

## 1.3控制台——分组显示

```javascript
console.group();//分组开始
console.log("第一条信息");
console.log("第二条信息");
console.groupEnd();//结束 
```

```javascript
var arr=[{"name":"Lily","age":20},{"name":"张三","age":30},{"name":"李四","age":40}]
for(i in arr){
    console.group(i);
    	console.log("姓名:"+arr[i].name);
    	console.log("年龄:"+arr[i].age);
    console.groundEnd();
}	
```

## 1.4控制台——console.dir()

console.dir()可以显示一个对象所偶的属性和方法  

## 1.5控制台——console.assert()

用来判断表达式或变量是否为真，如果结果为否，则在控制台输出一条相应信息，并且抛出一个异常。

```javascript
var result=0;
console.assert(result);
var year=2000;
console.assert(year==2011);
```

## 1.6控制台——console.trace()

用来追踪函数的调用轨迹

```javascript
1.function add(a+b){
	return a+b;
}
function add(a,b){
	console.trace();
	return a+b;
}
2.function add(a,b){
	console.trace();
	return a+b;
}
var x=add3(1,1);
function add3(a,b){return add2(a,b);}
function add2(a,b){return add1(a,b);}
function add1(a,b){return add(a,b);}
console.log(x);
```



## 1.7控制台——计时功能

用来显示代码的运行时间

```javascript
console.time("计时器一");
for(var i=0;i<1000;i++){
	console.log()
}
console.timeEnd("计时器一");
```

1.8 控制台——性能分析

性能分析(Profiler)就是分析程序各个部分的运行时间，找出瓶颈所在，使用的方法是console.profile()

```javascript
//假设有一个函数Foo(),里面调用了另外两个函数funcA和funcB(),其中funcA()调用10次，funB()调用一次
function Foo(){
    for(var i=0;i<10;i++){
        funcA(1000);
    }
    	funcB(1000);
}
function funcA(count){
    for(var i=0;i<count;i++){
        
    }
}
function funcB(count){
    for(var i=0;i<count;i++){
        
    }
}
//然后就可以分析Foo()的运行性能了
console.profile("性能分析器一");
Foo();
console.profileEnd();
```

```javascript
localStorage.name="Lily";
//缓存
```

```javascript
//storage缓存
//network运行加载时间
//sources对js设置断点 断点及到此处就不执行了
//performance性能
```





# FullPage

基于Jquery，支持前进后退上下键盘的控制，多个回调函数，支持手机、平板触摸事件，支持CSS3动画，支持缩放，可以设置滚动宽度、背景颜色、滚动速度、循环选项、回调、文本对齐方式等。

兼容性：jquery1.7以上版本

浏览器兼容：IE8+，chrome，Firefox，Opera

## 1.fullpage的生产环境（环境搭建）

因为fullpage是基于Jquery的，需要引入有fullpage的css和js，css直接link正常引入，引入js需要script，但前提是先引入Jquery，它必须要在Jquery的下面

fullpage.css-->jquery-->jquery-ui-->fullpage.js

## 2.基本结构

```html
<div id="fullpage">
   <div class="section">
       <h3>第一屏</h3>
    </div>
    <div class="section">
       <h3>第二屏</h3>
    </div>
    <div class="section">
       <h3>第三屏</h3>
    </div>
    <div class="section">
       <h3>第四屏</h3>
    </div>
</div>
<!--
每个.section代表一屏，默认显示“第一屏”，中间可以插入页面内容，section中内容默认水平居左垂直居中，可以使用CSS设置背景色以及背景图片
调用fullpage.js相关方法
基础方法：
<script type="text/javascript">
	$(document).ready(function(){
		$("#fullpage").fullpage();//该方法实现整屏滚动效果
	})
</script>

-->
```

## 3.带左右切换效果的整屏切换

```html
<div id="fullpage">
   <div class="section">
       <h3>第一屏</h3>
   </div>
    <div class="section">
       <h3>第二屏</h3>
    </div>
    <div class="section">
       <div class="slide">第三屏第一屏</div>
       <div class="slide">第三屏第二屏</div>
       <div class="slide">第三屏第三屏</div>
       <div class="slide">第三屏第四屏</div>
    </div>
    <div class="section">
       <h3>第四屏</h3>
    </div>
</div>
可以在.section元素内加入.slide元素，实现横屏切换效果
```

## 5.Fullpage初始化参数

配置选项采用Json格式，用来对fullpage()方法进行设置，通过参数的设置，可以指定全屏滚动的不同效果

fullpage里面写属性和方法的时候必须要遵循对象的方式

```
$("选择器").fullpage({
	name1.value1;
	name2.value2;
})
```

属性：值，属性：值，方法名：function(){}

颜色必须加引号包括rgba

easing:easeInQuart 设置滚动方式，默认值easeInQuart，设置该参数需要引入jquery.easing.min,js文件

### 5.1属性

* loopBottom:滚动最底部时是否滚回顶部 默认值:false

* loopTop:滚到最顶部时是否返回顶部 默认值:false

* controlArrowColor:#fff 左右滑块的箭头的背景颜色

* slidesColor:只要带s的就要以数组的方式来表示

  slidesColor:["#f00","#fff","#f0f];

* anchors:["page1","page2","page3"];定义锚链接，数组元素为页面对应锚链接的名称

* menu 绑定菜单 设置的相关属性与anchors的值对应后，菜单可以控制滚动

* scrollingSpeed:700 滚动速度，单位为毫秒，默认值700

* paddingTop:0 设置每屏下内边距，默认值0

* paddingBottom:0 设置每屏上内边距，默认值0

* keyboardScrolling:true 设置方向键导航，默认值true

* verticalCentered:true 内容是否垂直居中

* resize:false

* slidesColor:设置背景颜色

* autoScrolling:true 是否使用插件的滚动方式，如果选择false，则会出现浏览器自带的滚动条

* scrollOverflow:false 内容超过满屏后是否显示滚动条

* **continuousVertical:false 是否循环滚动**，与loopTop及loopBottom不兼容

* easing:easeInQuart  滚动动画方式

* loopHorizontal:true  设置左右滑块是否循环滚动，默认值true

* **css3:false  是否使用CSS3 transforms 滚动**

## 6.绑定菜单导航

```html
<ul id="menu">
    <li data-menuanchor="page1"><a href="#page1">第一屏</a></li>
    <li data-menuanchor="page2"><a href="#page2">第二屏</a></li>
    <li data-menuanchor="page3"><a href="#page3">第三屏</a></li>
    <li data-menuanchor="page4"><a href="#page4">第四屏</a></li>
</ul>
```

```javascript
//fullpage绑定
$("#menu").fullpage({
    anchors:["page1","page2","page3","page4"]，
    menu:"#menu"
})
```

当你想刷新后默认第一个按钮加上样式，可以在浏览器中找到他的样式，然后在css中直接用它自己给出的类别选择器来指定即可

```css
#menu li.active a{
    background-color:#a43;
}
```



## 7.项目导航

项目导航由fullpage()中的参数进行设置

* navigation:false 是否显示项目导航，默认值false，不显示
* navigationPosition:"right" 项目导航的位置，可选left和right
* navigationColor:#000  项目导航的颜色
* navigationTooltips:["第一屏","第二屏","第三屏","第四屏"];指向项目导航时出现的提示信息

### 7.1左右滑块项目导航

* slidesNavigation:false 设置是否显示左右滑块项目导航
* slidesNavPosition:"bottom"  设置左右滑块项目导航的位置，可选top和bottom
* controlArrowColor:"#fff"  设置左右滑块箭头的颜色

## 8.Fullpage方法函数

这些函数是在插件初始化外调用的，不同于回调函数，且不受参数的影响

* moveSectionUp()

  设置section向上滚动

  $.fn.fullpage.moveSectionUp();

* moveSectionDown()

  设置section向下滚动

  $.fn.fullpage.moveSectionDown();

* moveSlideRight()

  设置Slide向右滑动

  $.fn.fullpage.moveSlideRight();

* moveSlideLeft()

  设置slide向左滑动

  $.fn.fullpage.moveSildeLeft();


## 9.Fullpage回调函数

如果想要更加详细的控制Fullpage，就需要使用回调函数

* afterLoad(anchorLink,index)

  滚动到某一屏的回调函数，接受anchorLink和index两个参数

* anchorLink是锚链接的名称

  **index是section的索引，从1开始计算**

* onLeave(index,nextIndex,direction)

  滚动前的回调函数(离开当前页面时)

* index是离开的“页面”的序号，从1开始计算

* nextIndex是滚动到的“页面”的序号

* direction判断往上滚动还是往下滚动

* **slide的索引是从0开始的**

```javascript
$(document).ready(function(){
    $("#fullpage").fullpage({
        controlArrowColor:"raba(0,0,0,0.4)",
        slidesColor:["#fff","#ff0","#f0f","#ff0"],
        anchors:["page1","page2","page3","page4"],
        menu="#menu",
        slidesNavigation:true,
        slidesNavPosition:"top",
        afterLoad:function(anchorLink,index){
        	if(index==3){
                $(".section3").find("h1").animate({"left":"50%","margin-left":"-50px"},2000)
            }
    	},
         onLeave:function(index,nextIndex,direction){
             if(index==3){
                 $(".section3").find("h1").animate({"left":"-100px","margin-left":"0px"},2000)
             }
         }
    });
	$(".bot").click(funciton(){
         $.fn.fullpage.setAllowScrolling(false,down);
     })
})
```

* afterRender()

  这个回调函数知识在生成页面结构的时候调用。这是要用来初始化其他插件或删除任何需要的文件准备好代码的回调

  效果只有一次

* afterSlideLoad(anchorLink,index,slideAnchor,slideIndex)

  滚动到某一水平滑块后的回调函数，与afterLoad类似，接收anchorLink、index、slideIndex、direction4个参数

* onSlideLeave(anchorLink,index,slideIndex,direction,nextSlideIndex)

  某一水平滑块滚动前的回调函数，与onLeave类似，接收anchorLink、index、slideIndex、direction、nextSlideIndex5个参数。slideIndex


# 响应式布局

优雅降级——高版本——向下兼容

渐进增强——低版本——向上兼容



响应式布局应该是一种弹性的栅格布局，不同尺寸下弹性适应

* viewport 分为三种
* visual viewport 可视化  移动端  window.innerWidth来获取
* layout viewport 整个的宽度  PC端    document.documentElement.clientWidth来获取
* ideal viewport  理想    把以上两种结合起来成为理想布局
* document.documentElement.clientWidth指的是Body的宽度而window.innerWidth是屏幕实际宽度

```html
<!--使用viewport meta标签在手机浏览器上控制布局-->
<meta name="viewport" content="width=device-width宽度,initial-scale=1.0缩放,maximum-scale=1.0最大缩放,user-scalable=0不允许">
<!--通过快捷方式打开时全屏显示-->

```

**什么是响应式开发：针对不同的显示设备，显示分辨率进行的响应**

**实现响应式的方式：viewport** 

**结合@media来实现-->不同的屏幕尺寸或者是分辨率还有设备**

min-width，max-width

```css
body{
	background-color:#f00;
}
@media only screen and(max-width:1024px){/*写最大的时候要从大往小写 否则写在最下main的值会覆盖上面的值，反之，写最小的要从小往大写*/
    body{
        background-color:#0f0;
    }
}
@media only screen and(max-width:760px){
    body{
        background-color:#ff0;
    }
}
```

```css
除了使用上面的这种方式还有下面这种 通过每个css文件进行不同大小的设置
@media （min-device-width:1024px） and （max-width:989px），screen and （max-device-width:480px），（max-device-width:480px） and （orientation:landscape），（min-device-width:480px） and （max-device-width:1024px） and （orientation:portrait） {srules}

@media only screen and (min-width:320px){
    css的样式    
}

<link rel=“stylesheet” type=“text/css” media=“only screen and （max-width： 480px），only screen and （max-device-width： 480px）” href=“link.css”/>
```







# bootstrap

## 第一章 基本原理和布局

### 1.1 环境搭建

**首先引入bootstrap.css其次引入Jquery文件然后引入Bootstrap.js**

```
如果使用bootstrap必须要在head中添加
<meta name="viewport" content="width=device-width,initial-scale=1.0">
```

### 1.2容器

如果固定宽度container是居中显示的，如果是百分百的时候是靠左

如果想要用Bootstrap那么最外层的类别选择器不是container就是container-fluid

```html
<div class="container"></div>居中显示
<div class="container-fluid"></div>100%宽度，占据全部视口(viewport)
```

### 1.3 栅格系统

栅格系统原理：利用的是响应式来实现的，会把一行平均最多划分为12列，然后根据不同的尺寸进行响应的设置，有xs()的情况下，sm()，md()，lg()

会把一行划分为十二列

行row 列col

-col-尺寸-占的列（写的是占十二列里面的几列）

手机用.col-xs-4   <768px

平板.col-sm-4    >=768px

笔记本.col-md-4 >=992px

台式.col-lg-4	  >=1200px

### 1.4 列偏移

使用.col-md-offset-4(前面空的列数)

### 1.5 列排序

通过使用.col-md-push-n和.col-md-pull-n类就可以很容易的改变列的顺序

```html
<div class="row">
  <div class="col-md-9 col-md-push-3">.col-md-9 .col-md-push-3</div>
  <div class="col-md-3 col-md-pull-9">.col-md-3 .col-md-pull-9</div>
</div>
```

### 1.6 排版

针对的是标题h1~h6

直接写标记就会有样式

```html
	    <h1>学习使我快乐<small>学习使我快乐</small></h1>
        <h2>学习使我快乐<small>学习使我快乐</small></h2>
        <h3>学习使我快乐<small>学习使我快乐</small></h3>
        <h4>学习使我快乐<small>学习使我快乐</small></h4>
        <h5>学习使我快乐<small>学习使我快乐</small></h5>
        <h6>学习使我快乐<small>学习使我快乐</small></h6>
<small></small>被设置为父容器字体大小的 85%
```

### 1.7 表格

在table标签中加上.table类即可

```
条纹状表格 .table-striped
带边框的表格 .table-bordered
鼠标悬停	.table-hover
紧缩表格	.table-condensed

状态类：.active 鼠标悬停在行或单元格上时所设置的颜色
	   .success 标识成功或积极的动作
	   .info	标识普通的提示信息或动作
	   .warning	标识警告或需要用户注意
	   .danger	标识危险或潜在的带来负面影响的动作
```

### 1.8 表单

一个.form-group是一组

给input加上form-control让他变为bootstrap中的样式

```html
<form>
  <div class="form-group">
    <label for="exampleInputEmail1">Email address</label>
    <input type="email" class="form-control" id="exampleInputEmail1" placeholder="Email">
  </div>
  <div class="form-group">
    <label for="exampleInputPassword1">Password</label>
    <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
  </div>
  <div class="form-group">
    <label for="exampleInputFile">File input</label>
    <input type="file" id="exampleInputFile">
    <p class="help-block">Example block-level help text here.</p>
  </div>
  <div class="checkbox">
    <label>
      <input type="checkbox"> Check me out
    </label>
  </div>
  <button type="submit" class="btn btn-default">Submit</button>
</form>
```

#### 调整列尺寸

placeholder是默认在文本框中的内容

```html
<div class="row">
  <div class="col-xs-2">
    <input type="text" class="form-control" placeholder=".col-xs-2">
  </div>
  <div class="col-xs-3">
    <input type="text" class="form-control" placeholder=".col-xs-3">
  </div>
  <div class="col-xs-4">
    <input type="text" class="form-control" placeholder=".col-xs-4">
  </div>
</div>
```

### 1.9 按钮

```html
<a class="btn btn-default" href="#" role="button">Link</a>
<button class="btn btn-default" type="submit">Button</button>
<input class="btn btn-default" type="button" value="Input">
<input class="btn btn-default" type="submit" value="Submit">
```

#### 按钮的尺寸

```
.btn-lg	大按钮
.btn-default	默认尺寸
.btn-sm	小按钮
.btn-xs	超小按钮
```

#### 激活状态

添加.active类

```html
<button type="button" class="btn btn-primary btn-lg active">Primary button</button>
<button type="button" class="btn btn-default btn-lg active">Button</button>
```

#### 禁用状态

添加disabled属性并将值设置为disabled

```html
<button type="button" class="btn btn-lg btn-primary" disabled="disabled">Primary button</button>
<button type="button" class="btn btn-default btn-lg" disabled="disabled">Button</button>
```

#### 关闭按钮

```html
<button type="button" class="close" aria-label="Close"><span aria-hidden="true">&times;</span></button>
```

#### 三角符号

```html
<span class="caret"></span>
```



### 1.10图片形状

```html
<img src="..." alt="..." class="img-rounded">圆角正方形无边框
<img src="..." alt="..." class="img-circle">圆形
<img src="..." alt="..." class="img-thumbnail">边框圆角，形状正方形
```

### 1.11 默认分页

```html
<nav aria-label="Page navigation">
  <ul class="pagination">
    <li>
      <a href="#" aria-label="Previous">
        <span aria-hidden="true">&laquo;</span>
      </a>
    </li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li>
      <a href="#" aria-label="Next">
        <span aria-hidden="true">&raquo;</span>
      </a>
    </li>
  </ul>
</nav>
```

#### 禁用和激活状态

```html
<nav aria-label="...">
  <ul class="pagination">
    <li class="disabled"><a href="#" aria-label="Previous"><span aria-hidden="true">&laquo;</span></a></li>
    <li class="active"><a href="#">1 <span class="sr-only">(current)</span></a></li>
    ...
  </ul>
</nav>
```

#### 尺寸

```html
<nav aria-label="..."><ul class="pagination pagination-lg">...</ul></nav>
<nav aria-label="..."><ul class="pagination">...</ul></nav>
<nav aria-label="..."><ul class="pagination pagination-sm">...</ul></nav>
```

### 1.12 下拉菜单

```html
下拉菜单.dropdown
<div class="dropdown">
  <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown" aria-haspopup="true" aria-expanded="true">
    Dropdown
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenu1">
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li><a href="#">Something else here</a></li>
    <li role="separator" class="divider"></li>
    <li><a href="#">Separated link</a></li>
  </ul>
</div>
```

```html
向上弹出的菜单.dropup
<div class="dropup">
  <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu2" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
    Dropup
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenu2">
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li><a href="#">Something else here</a></li>
    <li role="separator" class="divider"></li>    <!--分割线-->
    <li><a href="#">Separated link</a></li>
  </ul>
</div>
<!--
<li class="disabled"><a href="#">Disabled link</a></li>  禁用的菜单项
-->
```























