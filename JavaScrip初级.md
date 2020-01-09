# 第一章 JavaScript入门

对象 函数 变量

语言：面向对象>面向过程>基于对象

基于对象：基于window对象、依附于html

## ***1.1 浏览器架构回顾

**用户界面：显示在浏览器上面的页面**

​	UI后端：元素具体应该显示在什么位置

**浏览器引擎：使浏览器运行**

​	**数据存储：存储数据的**

**浏览器内核：**解析JS和CSS的内容

​	网络：是否有网络

​	JS解析器：解析JS

​	UI后端：元素具体应该显示在什么位置

**JS与JScript都遵循ECMAScript标准(es5)**

## 1.2 javascript在网站中的应用

* 网页中的特效

* 表单验证

* ajax（高级）

* html5（高级）

## 1.3 javascript的概念以及特点

javascript是一种基于对象和事件驱动并具有安全性能的脚本语言。

脚本编写语言、基于对象的语言、简单性、安全性、动态性、跨平台性

## 1.4  javascript引入方式

script标记可以在任何地方写	两者不能混用

### 1.4.1 内嵌式

```html
<script type="text/javascript">
	js代码
</script>
```

### 1.4.2 外链式

将代码保存在新建的js文件中

```html
<script type="text/javascript" src="../js/index.js"></script>
```

### 1.4.3 html、css、js加载顺序：

js放在最后：加载到js时，浏览器停止对html和css的加载

## 1.5. javascript的注释

单行//

多行/* */

## 1.6. java调试工具

```javascript
console.log("好好学习");
在调试器上打印出来
document.write("hhh");
打印在页面中
alert();
弹出框
```

# 第二章 javascript变量及数据类型

## 2.1变量的概念

1.变量是存取数据的内存空间

内存：运行中程序数据暂存空间

2.变量的命名规则

javascript变量的命名规则：

以字母或下划线开头可以包含字母数字下划线，不能包括特殊字符（空格@&等）

不能使javascript关键字和保留字

## 2.2 变量的创建及初始化方法

变量的创建/声明/定义方法：

方法一：先创建后使用

```javascript 
var x; 创建变量
x=20;使用变量
```

方法二：直接使用由系统创建

```javascript
y=9;
```

## 2.3 常用数据类型

**1.数值型（Number）：整型和实数**

3  2.32  NaN:非数值，数值类型

**2.布尔型（Boolean）：true false**

布尔型可以做逻辑运算

**3.空类型:Undefined/Null**

undefined：变量没有赋值

null：对象为空

**undefined+数值=NaN**

变量为赋值

**4.字符串型（String）：凡是单引号或双引号包裹的内容都是字符串**

**5.object对象**

**6.array数组**

**7.类型测试typeof**

返回数据类型

typeof NaN	//number

typeof 3	//number

typeof "abc"	//string

typeof null	//object

typeof undefined	//undefined

**8.类型测试instanceof**

返回True,False

```javascript
console.log(x instanceof Boolean);	首字母大写
```

## 2.4理解字符串

字符串：+作为的是字符串连接符

数值：+作为加法运算符

数值和字符串：强制将数值强制转换成字符串 进行字符串连接

除了+之外做其他运算结果都是NaN

## 2.5 变量交换

z=x	x=y	y=z

# 第三章 javascript运算符和表达式

## 3.1表达式的概念

由运算符连接操作数组成的式子，不管运算符多长，最终是一个值。

例如2+3*3/5+6

## 3.2算术运算符

+、-、*、/、-负数、自增++、自减--

**++i	先自加再进行其他的运算**

**i++	先运算再加**

**运算的时候i++只计算i的值，++i算++i后的值	不管i++还是++i他们自身的值都是往上+1的 不影响本身 影响运算结果**

## 3.3比较运算符

=：赋值

**等于==：只比较值不比较数据类型**

**严格全等===：既比较值又比较数据类型**

不等于!=

严格不等于!==

大于>

小于<

大于等于>=

小于等于<=

## 3.4逻辑运算符

返回值为逻辑值：True和False

逻辑与&&：都为真才是真

逻辑或||：一个是真即为真，都为假才为假

逻辑非!：取反	真是假 假是真

## 3.5各种进制转换

2进制、10进制、16进制

8421

## 3.6位运算符

按位与&（全为1则为1）

按位或|（有1为1，全0为0）

按位异或^（不同为1，同为0）

位非运算~

左移位运算符<<，实现整体向左移动补0的功能

右移位运算符>>，当移动的是有符号数，左边空出的位用数的符号位填充。向右移动超出的位将被丢弃

无符号右移位>>>，当数是无符号数时，右移后在左边空出的位上填充0

## 3.7条件运算符

表达式?值1:值2

表达式成立执行值1	不成立执行值2

```javascript
3>2?console.log("3是大于2的"):console.log("3是不大于2的")
```

```javascript
:alert("")	弹出框
```



## 3.8运算符优先级

```
+=	例如a+=2	a=a+2
```

```
-=	 例如a-=2	a=a-2
```

```javascript
*=   例如a*=2	a=a*2
```

```javascript
判断奇偶
var i=11;
if(i%2==0){
	console.log(i+"是偶数");
}
```

# 第四章 javascript结构

## 4.1顺序结构

所有语句全部从上往下，逐条执行（没有结构就是顺序结构）

### 4.1.1 程序流程图

圆角矩形：程序开始或结束

菱形：判断条件

矩形：执行语句

箭头：程序执行方向

## 4.2单分支结构

单分支：要么做，要么不做

```javascript
if(条件){
  语句；
  语句；
}
```

## 4.3双分支

双分支

```javascript
if(条件){
  语句；
  语句；
}else{
  语句;
  语句;
}
```

```javascript
var i=11;
if(i%2==0){
	console.log(i+"是偶数");
}else{
	console.log(i+"是奇数");
}
```

```javascript
var i=11;
if(i%2==0){
	if(i%5==0){
		console.log(i+"既是5的倍数又是2的倍数");
	}else{
		console.log(i+"是2的倍数但不是5的倍数");
    }
}else{
    if(i%3==0){
        console.log(i+"是3的倍数但不是2的倍数");
    }else{
        console.log(i+"既不是3的倍数又不是2的倍数");
    }
}
```

```javascript
for(var i=0,j=0;i<6,j<10;i++,j++){

}
console.log(i+j);
//跟j有关系，结果为20 循环继续的判断依据以分号前的最后一项为准
```



## 4.4多分支结构

```
if(条件){
  语句；
  语句；
}else if(条件){
  语句;
  语句;
}else if(条件){
  语句;
  语句;
}else{		最后一个结束语句不需要判断的时候直接执行语句。
  语句;
}
```

作业：百分制 100 负数的时候 0的时候 90优秀 80良好 70还行 60及格 0完蛋了 小于60不及格

## 4.5多选一

```
switch(表达式/变量){
	case 值1：
	语句;
	break;
	case 值2:
	语句;
	break;
	default:	都不是的情况下
	语句;
}
```

switch后写表达式的情况下，下面的case值也要用表达式表示。语句不要产生矛盾。

## 4.6 for循环

```javascript
for(循环初始化;条件;增量){
	语句;
	语句;
}
for(var i=1;i<10;i++){
	console.log(i)
}
document.write(i+"<br>");打印换行。因为浏览器会直接解析Html，直接将Html作为字符串输出即可。
```

```javascript
for(var i=1;i<=16;i++){
	console.log("* ")
	if(i%4==0){
		console.log("<br>");
	}
}
```

```javascript
for(var i=1;i<=4;i++){
	for(var j=1;j>=i;j++){
        document.write("* ");
    }
    document.write("<br>");
}
```

j>=5-i	因为j是控制内循环列

找i与j的关系，＋、-、*、/	加减乘除

```javascript
for(var i=1;i<=4;i++){
	for(var j=1;j<=4;j++){
		if(j>=5-i){ 	j<=5-i	j<=i	j>=i
			document.write("*");
		}else{
			document.write("&nbsp;");
		}
	}
	document.write("<br>");
}
```

菱形135 

```javascript
var sum=0;
for(var i=1;i<=100;i++){
	sum=sum+i;
}
document.write(sum);
```

```javascript
for(var i=1;i<=4;i++){
	for(var j=1;j<=4;j++){
        if(j<=i){
         	document.write("("+i+","+j+")");   
        }
	}
		document.write("<br>");
}
```

99乘法表

## 4.7 while循环

直到型循环，直到条件为false时才不执行。

```javascript
while(条件){
	语句;
	增量;
}
```

* while与do-while区别

  **1.正常情况下，如果条件不成立的情况下do是执行的，while是不执行的，即do至少执行一次**

  2.while会比do-while多循环一次

  3.do-while比while更容易进入死循环

## 4.8 do-while循环

类似于while，先运行语句再判断条件

```javascript
do{
	语句;
	语句;
}while(条件)
```

```javascript
var i=1;
do{
	document.write(i+"<br>");
}while(i<0)
```

## 4.9 break continue

continue:终止本次循环，继续下一次循环

break:终止

```javascript
for(var i=1;i<=10;i++){
	if(i==8){
	continue;
}
	document.write(i+"<br>");
}
```

### 4.9.1标记法

```javascript
打印100个7的倍数
var i=1;
var j=0;
while(i>0){
	if(i%7==0){
		document.write(i+"<br>");
		j++;
	}
	if(j==100){
		break;
	}
	i++;
}
```

# 第五章 javascript函数

## 5.1 自定义函数

函数是完成置顶功能的程序段，可以反复调用，减少代码冗余。

### 5.1.1 创建自定义函数

1.函数定义/声明/创建

```
function 函数名(形参,形参,...){
	语句;
	语句;
	语句;
	....
	[return表达式/值;]
}
```

onclick="test()"

2.调用函数

```
函数名（实参，实参，...）;
```

**说明：函数如果没有调用，函数自己不会自己调用**

## 5.2 无参函数

函数没有参数，不需要参数，一般指完成固定的功能。

## 5.3 单参函数

只有一个参数

## 5.4递归函数

函数本身自己调用自己

## 5.5 匿名函数

没有函数名称的函数

**只能在js里面调用，因为没有名字**

```javascript
(function(){
	document.write("好好学习");
})()

(function(a,b){
	document.write(a+b);
})(2,3)
```

## 5.6 构造函数

用来创建对象

```javascript
function person(){
	this.name="Lily";
	this.sex="女";
}
```

## 5.7回调函数

a和b就是回调函数

```javascript
function add(x,y){
	document.write(x+y);	//return x+y;
}
function a(){
	return 2;
}
function b(){
	return 3;
}
add(a(),b())
//document.write(add(a(),b()))
```

## 5.8自调函数

```
(function(){
	document.write("Hello");
})()
```

**全局变量，函数内外都有效**

**函数在读的时候优先读局部的变量，因为函数执行的时候先读，读完后才知道变量有值**

函数先读，读完后释放

```javascript
var a=3；
function test(){
	document.write(a);
	var a=2;	/*a=2;*/
	document.write(a);
}
test();
document.write(a);
```

**加var undefined23	不加322**

**局部中var上面打印的值都是undefined**

## 5.9内部(私有)函数

在函数内部的函数

只能在作用域范围内调用

```javascript
function a(){
	console.log(1)
	function b(){
		console.log(2)
	}
	b();
}
a();
```

## 5.10 带返回值函数

函数定义中有return语句。谁调用的它，返回给谁。可以是数值、字符串、对象

```javascript
function test(){
	c=2+3;
	return c;	//test()=c
}
test()
document.write(test());
```



## 5.11 能重写自己的函数

由于一个函数可以返回

第一次调用的值为3之后再调用50

```javascript
function test(){
	document.write(3",");
	test=function(){
		document.write(50);
	}
	test();
}
test();
```

## 5.12 系统(内置)函数

* URL编码函数:encodeURI()

* URL解码函数:decodeURI()

* **数据类型转换--转换为整数:parselnt();转换失败返回NaN**

* **数据类型转换函数--转换为实数:parseFloat();转换失败返回NaN**

* 判断是否是非数字:is NaN();

  --is NaN parseFloat

* eval():计算字符串表达式的值或者写字符串的js语句

# 第八章 内置对象

内置：8个

Bom:

Dom:

* 内置：

  属性->变量（静态特性）

  方法->函数（动态行为）

## 8.1 内置对象

Sring(字符串对象)

Array(数组)

Math(数学)

Date(时间)

Number(数字)

Function(函数/方法)

RegExp(正则表达式)

Error(异常)

## 8.2 String对象--属性

### 8.2.1 String对象--字符串对象

说明：凡是用""或''包裹的都是字符串，表单文本框所有内容都是字符串

```javascript
var str="HelloWorld";
var strNew= new String("Hello");
console.log(typeof str);	/*返回值string*/
console.log(typeof strNew);		/*返回值object,因为是借助对象创建的*/
```

### 创建对象的方式

​	---直接赋值

​	---new String();构造函数创建 

**1.length属性	长度 str.length()**

```javascript
var str="我是来自朗科网络网站58班的一个学生";	//写一个字符串，如果这个字符串大于10的话就截取他的十个数输出											后面连接上省略号，如果不大于10就直接输出。
if(str.length>10){
	document.write(str.substr(0,10)+"...");
}else{
	document.write(str);
}
```

**2. prototype属性(原型) 绑定在string上	为对象增加新的方法**	覆盖旧方法实现新功能

每一个对象共有的属性就是prototype属性

```javascript
var str="Hello";
var strNew="好好学习，天天向上";
String.prototype.wb="我是尾巴";
console.log(str.wb);
console.log(strNew.wb);



x="abc";
String.prototype.fn=function(){
	alert("测试");
}

```

## 8.3 String对象--方法

1. ***charAt():返回字符串中的第n个字符	从0开始**

2. charCodeAt():返回字符串中第n个字符的Unicode编码

3. concat():连接字符串	+

4. fromCharCode():

5. ***indexOf():检索字符串    有的话返回索引值从0开始	没有的话返回-1	重复的话返回的是第一个的索引值**

6. ***lastIndex():从后向前检索一个字符串	索引值不变 从后面开始就近**

7. localeCompare():相当于==	===	相等返回0  少或多返回-1和1

8. ***slice():截取取一个字符串 slice(从哪个索引值开始0，到哪个索引值结束2：但是不包含2) slice(0,2)到2为止 只有开始值：从开始值截到最后。**

9. ***substr():截取字符串**	**substr(开始的索引值，个数)**	substr(1,6)	**不写个数的情况下截到结束为止**	**负数是从后往前截** 

   ```javascript
   /*从-3个开始截取3个字符*/
   function fileGet(){
       var a="nihaoa"
       console.log(a.substr(-3,3));	-3为倒数第三个开始截取三个
   }
   
   
   function fileGet(){
       var a=document.myForm.f1.value
       if(a.substr(-3,3)=="gif"||a.substr(-3,3)=="jpg"||a.substr(-3,3)=="png"){
           alert("图片上传成功");
       }else{
           alert("文件类型错误");
       }
   }
   ```

10. substring():返回字符串的一个子串	跟slice一样	不能使用负数

11. **toLowerCase():将字符串转换成小写**

12. **toUpperCase():将字符串转换成大写**

13. valueOf():返回字符串

14. **split():按照指定的符号进行分割成一个数组**

    ```javascript
    var str="a&b&c&d"	/*如果什么都没有的情况下str="abcd";split("")引号内什么都不放*/
    console.log(str);
    var arr=str.split("&");
    console.log(arr);
    ```

* 其他类型的数据转换为字符串

  tostring():返回字符串

## 8.4 Array对象

数组存放的是一组的数据

### 8.4.1 创建数组

```javascript
1. var 对象名=new Array();/*只知道当前对象是数组对象，但是没有长度，没有值*/ typeof返回值为object 复合数据类型
2. var 对象名=new Array(4);/*知道长度但是不知道值,存放的个数/长度*/
3. var 对象名=new Array(值1，值2，值3，值4); /*长度和值都有，长度为4*/
4. var 对象名=[值1,值2,值3,值4];	/*建议使用*/
```

### 8.4.2 遍历数组

```javascript
直接打印console.log(arr);输出的是长度和内容，方便传值时查看
```

```javascript
/*第一种方法*/
var arr=[1,2,3,4,5];
for(var i=0;i<arr.length;i++){
	console.log(arr[i]);
}
/*第二种方法 i是下标*/	
for(i in arr){
    console.log(arr[i]);
}
```

## 8.5 Array对象--属性

与String对象的属性一样

## 8.6Array对象--方法

1. join():将数组元素按指定分隔符连接起来，返回一个字符串

   ```javascript
   var arr=["a","b","c","d"];
   var str=arr.join("&");
   for(var i=0;i<arr.length;i++){
       	console.log(arr[i]);
   }
   ```

2. pop():删除并返回数组的最后一个元素(出栈)     先进后出原则

   ```javascript
   var arr=[1,2,3,4];	/*1 2 3*/
   arr.pop();
   for(var i=0;i<arr.length;i++){
   	console.log(arr[i]);
   }
   ```

3. push():给数组添加元素(入栈)

   ```javascript
   var arr=[1,2,3,4];	/*1 2 3 4 5*/
   arr.push(5);
   for(var i=0;i<arr.length;i++){
   	console.log(arr[i]);
   }
   ```

4. shift():删，移除数组中第一个元素-->会改变元素组

   ```javascript
   var arr=[1,2,3,4,5];	/*2 3 4 5*/
   arr.shift();			/*shift后的括号内为空*/
   for(var i=0;i<arr.length;i++){
       console.log(arr[i]);
   }
   ```

5. unshift():在数组头部插入一个元素，后面写多少就会在头部插入多少-->会改变元素组

   ```javascript
   var arr=[1,2,3,4,5];	/*9 2 3 47 1 2 3 4 5*/
   arr.unshift(9,2,3,47);
   for(var i=0;i<arr.length;i++){
       console.log(arr[i]);
   }
   ```

6. concat():连接数组-->不会改变原数组

   ```javascript
   var arr1=[1,2,3,4];			/*1 2 3 4 2 3 4 5*/
   var arr2=[2,3,4,5];
   var arr3=arr1.concat(arr2);
   for(var i=0;i<arr3.length;i++){
       console.log(arr3[i]);
   }
   ```

7. reverse():颠倒数组中的顺序-->会改变元素组

   ```javascript
   var arr=[1,2,3,4];	/*4 3 2 1*/
   arr.reverse();
   for(var i=0;i<arr.length;i++){
   	console.log(arr[i]);
   }
   ```

8. slice():截取

   ```javascript
   /*slice写法*/
   var arr=[1,2,3,4,5];	/*3 4*/	/*从下标为2的开始截取到下标为4但不包含4结束*/
   var arrNew=arr.slice(2,4);
   for(var i=0;i<arrNew.length;i++){
   	console.log(arrNew[i]);
   }
   /*splice写法*/
   var arr=[1,2,3,4,5];	/*3 4*/	/*开始下标，截取个数*/
   var arrNew=arr.splice(2,2);
   for(var i=0;i<arrNew.length;i++){
       console.log(arrNew[i]);
   }
   ```

9. sort():对数组元素进行排序--(按照第一个数字，以及个数排序)

10. splice():插入、删除、替换数组中的元素    **splice(开始下标，个数)**      替换：splice(2,2,6,7)-->6,7是要替换的数

    splice(下标,删除或替换的个数,~~~~替换或插入的值)

    ```javascript
    var arr=[1,2,3,4,5];	/*1 2 5*/	/*删除*/
    arr.splice(2,2);
    for(var i=0;i<arr.length;i++){
    	console.log(arr[i]);
    }
    
    var arr=[1,2,3,4,5];	/*1 2 6 7 5*/	/*替换*/
    arr.splice(2,2,6,7);
    for(var i=0;i<arr.length;i++){
        console.log(arr[i]);
    }
    
    var arr=[1,2,3,4,5];	/*1 2 6 7 3 4 5*/	/*插入从第下标为2后开始插入删除0个*/
    arr.splice(2,0,6,7);	
    for(var i=0;i<arr.length;i++){	
        console.log(arr[i]);		
    }
    ```

11. toString():把任意对象转换成字符串   

    ```javascript
    var arr=[1,2,3,4,5];
    var str=arr.toString();
    console.log(str);
    ```

12. 最大值最小值找法：把数组中的第一项既看成最大值也是最小值，对数组进行遍历，比较，赋值，完成

    ```javascript
    var arr=[2,4,1,67,92,45,37];	/*最大值*/
    var max=arr[0];
    for(var i=0;i<arr.length;i++){
    	if(max<arr[i]){
    		max=arr[i];
    	}
    }
    
    var arr=[2,4,1,67,92,45,37];	/*最小值*/
    var min=arr[0];
    for(var i=0;i<arr.length;i++){
    	if(min>arr[i]){
    		min=arr[i];
    	}
    }
    ```

13. **冒泡排序：大的不动，小的互换**

    需要对数组进行遍历i，拿数组中的第一项和之后的进行比较，再次对数据进行遍历j，在比较的时候第二次遍历的下标值始终从当前i+1开始，然后比较i和j的值，如果后面小那么两者位置交换，否则不动

    ```javascript
    var arr=[2,4,1,67,92,45,37];
    var m;
    for(var i=0;i<arr.length;i++){
       for(var j=i+1;j<arr.length.j++){
           if(arr[i]>arr[j]){	/*>从小到大，<从大到小*/
               m=arr[i];
               arr[i]=arr[j];
               arr[j]=m;
           }
       }
    }
    for(var i=0;i<arr.length;i++){
        console.log(arr[i]);
    }
    ```

14. **去重:为了避免连续重复使用j--因为删除了一个下标集体往前走一个**

    原理：1.两个遍历，第一个遍历-->选第一个数组项，第二个遍历-->比较数组项

    ​		   2.两个数组项进行比较，在比较的过程中，相等删除，删除索引值为j的，因为循环的是j

    ​		   3.如果有连续循环的话，删完之后需要让j-1，目的是再次比较当前的索引值

    ```javascript
    var arr=[57,68,24,1,3,68,3,3,3];
    for(var i=0;i<arr.length;i++){
    	for(var j=i+1;j<arr.length;j++){
    		if(arr[i]==arr[j]){
    			arr.splice(j,1);
    			j--;
    		}
    	}
    }
    for(i in arr){
    	console.log(arr[i]);
    }
    ```

    **去重:indexof()**

    ```javascript
    var arr=[57,68,24,1,3,68,3,3,3];
    var temp=[];
    for(var i=0;i<arr.length;i++){
    	if(temp.indexOf(arr[i])==-1){
    		temp.push(arr[i]);
    	}
    }
    console.log(temp);
    ```


### 购物车

* 原理：1.需要两个数组 pro、num

  ​		   2.add(str)这个方法就是用来把商品添加到pro，把数量添加到num，用str来代表添加的商品是谁

  ​		   3.pro中有没有str，如果没有的话让pro加上str，让num加上1

  ​		   4.对pro进行遍历，判断str是否存在于pro里，如果有的情况下让num加一，需要找的是商品对应的数量的下标

  ​		   5.就把pro的下标，找中间变量y，y就是用来存下标的，y=i

  ​		   6.所以y不能是大于等于0的，y=-1

  ​		   7.判断y是否等于-1，如果等于的话就让pro和num同时增加，让num[y]+=1

y=-1表示第一次没有按过的情况下 y=其他数的时候是直接添加数量 下标需要y来存储，记录当前商品的下标 给当前商品对应的数量加1         pro[ ]和str pro[i]==str

```html
	<button onclick="add('上衣')">上衣</button>
    <button onclick="add('帽子')">帽子</button>
    <button onclick="add('裤子')">裤子</button>
    <button onclick="add('鞋子')">鞋子</button>
    <button onclick="showcar()">显示购物车</button>
```

```javascript
var pro=[],num=[];//设定两个数组，一个放商品一个放数量
function add(str){//使用add这个方法 str是点击放在add中的商品
    var y=-1;//使用一个变量给他赋值为1目的是当有了这个商品的时候只需要找到他的下标就可以给他的数量+1
    for(var i=0;i<pro.length;i++){//遍历pro
        if(pro[i]==str){  //找到匹配的商品把下标赋给变量y
            y=i;
        }        
    }
    if(y==-1){//没有找到匹配的商品说明是第一次添加 所以y=-1
        pro.push(str);//把点击的这个str给到pro中
        num.push(1);//在商品的数量上面给他赋初值1
    }else{//找到匹配的商品 下标会变
        num[y]+=1;//给num+1
    }
}
function showcar(){//显示购物车按钮
    for(i in pro)//遍历数组Pro
    document.write(pro[i]+":"+num[i]+"<br>")
}
```

## 8.7 二维数组

```javascript
var arr=[["语文","数学","英语"],["政治","历史","地理"],["物理","化学","生物"]];
for(var i=0;i<arr.length;i++){
	for(var j=0;j<arr[i].length;j++){
		console.log(arr[i][j]);
	}
}
```

## 8.9 Math对象--属性

* PI属性

  返回圆周率(约等于3.14159)

## 8.10 Math对象--方法

内置对象中唯一的静态对象

1. random()返回0~1之间的随机数

   可以取到0但是取不到1

   ```javascript
   console.log(Math.random());
   //创建一个空字符串，循环次数为想要输出的位数，然后将随机数扩大十倍并向下取舍。
   var str="";
   for(var i=0;i<4;i++){
       str+=Math.floor(Math.random()*10);
   }
   document.write(str);
   ```

   ```javascript
   document.write("<img src='../img/0.png'>");		/*图片验证码*/
   var str="";
   for(var i=0;i<4;i++){
   	var j=Math.floor(Math.random()*10);
   	str+="<img src='../img/"+j+".png'>"
   }
   ```

   ```javascript
   <span id="d1"></span>
   
   function yzm(){
       var str="";
       for(var i=0;i<4;i++){
           var j=Math.floor(Math.random()*10);
           str+="<img src='../img/"+j+".png'>"
       }
       document.getElementById("d1").innerHTML=str;
   }
   yzm();
   ```

   减少加载时间的方式：减少与document之间的交互

2. floor(x)对数进行向下舍入

   ```javascript
   var arr=["0","1","2","3","4","5","6","7","8","9"];
   var str="";
   for(var i=0;i<4;i++){
       var j=Math.floor(Math.random()*10);
       str=str+arr[j];
   }
   document.write(str);
   ```

   

3. round(x)把数四舍五入到最接近的整数

4. abs(x)返回数的绝对值

5. ceil(x)对数进行向上舍入

## 8.11 Date对象--属性

new Date():构造函数创建

prototype属性

## 8.12 Date对象--方法

### 返回GET

1. getDate():从Date对象返回一个月中的某一天(1~31)
2. getDay():从Date对象返回一周中的某一天(0~6)
3. getMonth():从Date对象返回月份(0~11)       getMonth()+1
4. getFullYear():从Date对象以四位数字返回年份
5. getHours():返回Date对象的小时(0~23)
6. getMinutes():返回Date对象的分钟(0~59)
7. getSecond():返回Date对象的秒数(0~59)
8. getMilliseconds():返回Date对象的毫秒(0~999)

```javascript
var da=new Date();
var arr=["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
var y=da.getFullYear();
var m=da.getMonth()+1;
var d=da.getDate();
var day=da.getDay();
var h=da.getHours();
var mi=da.getMinutes();
var s=da.getSeconds();
document.write(y+"年"+m+"月"+d+"日"+arr[day]+" "+h+":"+mi+":"+s);
```

```javascript
/*还剩多少秒*/
var i=10,j;
function countDown(){
    if(i<=0){
        document.myForm.btn.disabled=false;
        document.myForm.btn.value="重新发送";
        i=10;
        clearTimeout(j);
    }else{
        i--;
        document.myForm.btn.disabled=true;
        document.myForm.btn.value="还剩"+i+"s";
        j=setTimeout(countDown,1000);
    }
}
```

```javascript
Var d=new Date();//2019-12-11如果是12-08如何判断这一位
r=d.getDate();
if(r<10){
  r="0"+r;
}
```

### 		设置SET

1. setDate():设置Date对象中月的的某一天(1~31)

2. setMonth():设置Date对象中月份(0~11)

3. setFullYear():设置Date对象中的年份(四位数字)

   ```javascript
   var da=new Date();
   da.setFullYear(2020);
   console.log(da.getFullYear());
   ```

4. setHours():设置Date对象中的小时(0~23)

5. setMinutes():设置Date对象中的分钟(0~59)

6. setSecond():设置Date对象中的秒钟(0~59)

7. setMilliseconds():设置Date对象中的毫秒(0~999)

8. setTime()以毫秒设置Date对象

### 转换为字符串TO

1. toString()把Date对象转换为字符串
2. toTimeString()把Date对象的时间部分转换为字符串
3. toDateString()把Date对象的日期部分转换为字符串
4. toUTCString()根据世界时间，把Date对象转换为字符串
5. toLocaleString()根据本地时间的格式，把Date对象转换为字符串
6. toLocaleTimeString()根据本地时间格式，把Date对象的时间部分转换为字符串
7. toLocaleDateString()根据本地时间格式，把Date对象的日期部分转换为字符串
8. UTC() 根据世界时间返回1970年1月1日到指定日期的毫秒数

当前系统

getMonth()真实的+1	getMonth()+1

## 8.13 Number对象

通过Number.上属性

**Number.NaN**

方法：

toString:把数字转换为字符串，

toFixed:toFixed(3) 四舍五入 

系统函数：parseInt()、parseFloat()

```javascript
var num=new Number(2);
console.log(typeof num.toString());

var num=new Number(2.6327);
console.log(num.toString());

var num=new Number(2.6327);
console.log(num.toFixed(3));		/*2.633*/
```

## 8.14 Function对象

```javascript
function(test形参){
	return a+b;
}
var 对象名=new Function("a","b","return a+b");
console.log(test(1,2));

function test(a,b){
    console.log(test.length);
    console.log(arguments.length);
    console.log(arguments[1]);
}
test(1,2)
```

属性

length--获取参数的个数

test.length--形参的个数

arguments.length--实参的个数---前面不用写对象名--存储的形式为数组--必须放到function里面否则无效

arguments属性

arguments.callee()方法 

```javascript
function test(n){	/*在函数内部调用自己*/
	console.log(n);
	argument.callee(n+1);
}
test(1)
```

```javascript
/*string:字符串对象
indexOf:有返回索引值，没有返回-1
CharAt:返回一个字符，根据索引值来判断的
slice:(起始的下标位置，结束的下标位置，但是不包含在内)
substr:(只有一个值,截到结束为止)、(负数从后往前截,个数)、(下标，个数)
split:按照指定的分隔符分开转换成字符串数组
length:判断当前字符串的长度的
案例:判断文字上传类型,超出显示省略号

Array:数组对象
push、unshift:添加,后,前
pop、shift:删、后、前
join:连接成字符串
splice:添加、替换、删除
案例:去重、排序、最大值、最小值、购物车

日期对象:Date
获取:get,月份始终是-1,星期是数组周日从0开始
设置:set
案例:倒计时、获取当前时间

Math:数学对象
PI
random、floor、ceil、round
案例:返回四位随机验证码、返回四位随机图片、返回-10到10的随机数

数值对象:Number
NaN:非数值
toString、toFixed

函数对象:Function
length:返回参数的个数
arguments:对象:代表的实参、用数组来存
callee:获取的是当前的函数
案例:面试题会出代码题
```

## 8.15 Error对象

Error对象的属性:

* name:错误类型(不同浏览器有差异，IE6/7/8有错误类型不同)
* number:错误号(仅IE支持)   (32位，高16位即其代码，低16位错误代码)
* message:错误信息(不同浏览器有差异)

1.new Error()   2.系统自动创建

```javascript
var error=new Error();  /*自己创建*/
error.message="错误信息";
```

try-catch异常处理优点:

* 防止用户看到不友好的系统错误
* 由于Error在不同的浏览器，报错信息有差异，可以使用try-catch进行统一报错信息，可以处理人为编写程序造成的异常，增强程序的健壮性

```javascript
try{			/*保证后面的代码正常运行*/
	错误；/*放在里面*/
}catch(e){					/*e-->Error 如果有错误的情况下这个对象是由系统自动创建的*/
	alert(e.message);					/*加if判断*/	/*message获取这个错误 但不能执行*/
}finally{
    /*最终执行的内容*/
}
```

```javascript
例题:
try{
	x=a;
}catch(error){
    e.message("错误信息");	/*不写的时候出来的是a is not defined 为了对用户更友好在								e.message中添加错误提示 */
	console.log(error.message);
}finally{
	a=3;
	a=x;
	console.log(x);
}
```

```javascript
/*例题*/
<form action="javascript:;" name="myForm">
    <input type="text" name="username">
    <input type="password" name="pwd">
    <input type="button" onclick="test()" value="登陆">
</form>

function test(){
    var user=document.myForm.username.value;
    var pwd=document.myForm.pwd.value;
    try{
        if(user!="admin" && user!="admin"){
            throw new Error("用户名或密码错误");
        }else{
            console.log("登陆成功");
        }
    }catch(e){
        console.log(e.message);
    }finally{
        document.myForm.username.value="";
        document.myForm.pwd.value="";
    }
}
```

## 8.16 RegExp对象

创建正则表达式对象的方式

* var reg=/表达式/对象的属性;

  例如 var reg=/ /;

* var reg=new RegExp('表达式'[,'对象的属性']);

  例如 var reg=new RegExp();

元字符：

* .	匹配任何字符
* \d  匹配任何数字
* \D  非数字字符
* \w  匹配数字、字母、下划线
* \W 非数字、字母、下划线
* \s   匹配空格(空白字符，tab换行符，return/enter)
* \S  非空白
* ^    以……开始
* $    以……结束
* |     或

限定符：

*  *，   0或多次
* +,      1或多次  最少一次
* ?,      0或1次    最多一次
* {n}     恰好出现n次
* {n,m}  最少n次，最多m次  n~m之间  {6，12} 6-12个字符之间
* {n,}     至少出现n次
* {,m}    最多出现m次

```javascript
手机号
/^(13|14|15|16|17|18|19)\d{9}$/
/^(1[3,9])(\d{9})$/
```

转义字符：

```
\.  出来的就只是.
\+  +
\0  空字符
\cX 与x对应的控制字符(ctrl+x)
\t  tab 水平制表符
\r  回车
\n  换行
\f  换页
\v  垂直制表符
```

范围类：

```javascript
[a-z]
[A-Z]
[0-9]
如果表示数字[0123456789]
```

### RegExp对象的属性

```javascript
g:gloabal  全文搜索
i:ignore Case  忽略大小写
m:multiplelines  多行搜索
例:var reg=/j.*/ig;
  reg.global;	为true
```

### RegExp对象的方法

* test(字符串)方法，如果正确返回true，错误返回false

  reg.test(内容)

  ```javascript
  var reg=/^(1[3-9])(\d{9})$/
  var phoneNum=1234567897;
  console.log(reg.test(phoneNumber));
  ```

  ```javascript
  var reg=/^(1[3-9])(\d{9})$/
  var phoneNum=1234567897;
  if(reg.test(phoneNum)){
  	console.log("匹配成功");
  }else{
  	console.log("手机号输入有误");
  }
  ```

  ```javascript
  var reg=/^(1[3-9])(\d{9})$/
  document.getElementById("phone").onkeyup=function(){
  	if(reg.test(this.value)){
  		this.nextElementSibling.innerHTML="输入正确";
           this.nextElementSibling.className="success";
  	}else{
  		this.nextElementSibling.innerHTML="手机号输入有误";
           this.nextElementSibling.className="error";
  	}
  }
  ```

* match(要搜索的字符串)方法，可在字符串内搜索指定子字符串，并返回到一个数组中

* match(reg)方法，匹配一个或多个g正则表达式的字符串，返回到数组中

  ```javascript
  var str="张三,今天好好学习了吗？张三天天好好学习!!";
  var reg=/张./g;
  var arr=str.match(reg);
  console.log(arr);
  ```

* replace(要搜索的字符串，替换成什么字符串)方法，用于在字符串中用一些字符替换另一些字符

* replace(正则表达式，替换成什么字符串)方法，或替换一个与正则表达式匹配的子串

  ```javascript
  var str="张三,今天好好学习了吗？张三天天好好学习!!";
  var reg=/张./g;
  var strNew=str.replace(reg."李四");
  console.log(str);
  console.log(strNew);
  ```

* search(字符串)方法用于搜索字符串中指定的子字符串，返回第一次匹配的起始位置，没有匹配的返回-1

* search(正则表达式)或检索与正则表达式相匹配的子字符串，返回第一次匹配的返回-1

  ```javascript
  var str"张三,今天好好学习了吗？张三天天好好学习!!";
  var reg=/张./g;
  console.log(str.search(reg));
  ```

匹配邮箱 身份证号(1900年开始到2019) 用户名(字母数字下划线，并且字母或数字开头，6-12位)  密码(字母数字下划线.@&*，并且字母或数字开头，6-12) 手机

```javascript
var reg=/^([0-9a-zA-Z])+@([0-9a-zA-Z])+\.(com|cn)$/邮箱
var reg=/^[1-9]\d{5}(19|18)\d{2}(0[1-9])(1[0-2])(0[1-9]|1[0-9]|2[0-9]|3[0-1])\d{3}([0-9]|x|X)$/身份证
```

# 第九章 BOM对象

BOM代表浏览器对象

DOM代表文档对象

**在body里面写的是DOM，不在body里面写的是BOM**

BOM是包含DOM的

```javascript
/*
BOM:window、document、frames、history、location、navigator、screen
DOM(document):anchors、forms、images、links、location
*/
```

## 9.1 Window对象--属性

**不需要创建直接用就可以**

**innerHeight:当前整个窗口的实际高度(不包含工具栏和滚动条)

```
console.log(window.innerHeight);
```

**innerWidth:当前整个窗口的实际宽度(不包含工具栏和滚动条)

Length:设置或返回窗口中的框架数量

```javascript
console.log(window.length);		/*例子：浮动框架的数量*/
```

## 9.2 Window对象--方法

* **alert("提示信息");		主要基于window对象所以前面可以不加window**

* **confirm("提示信息");	有两个按钮一个按钮是确定(会有返回值:true)，一个按钮是取消(会有返回值:false)**

* **prompt("提示信息","默认值");**        **有一个输入框，一个确定(返回值为输入框中的值)，一个取消(返回值为空)**

  0-150成绩

* **window.open("URL","窗口名称","属性=值,属性=值,属性=值")     打开一个窗口**

  ```javascript
  /*使用形参与实参传递值*/
  window.open("product.html","procuct","width=200,height=200,left=200,top=200");
  ```

  ![](C:\Users\王加藤\Desktop\窗口特征.jpg)

* **print()  打印当前页面 打印机**

* **close() 关闭当前浏览器页面**

* resizeBy() 将窗口调整宽度和高度 resizeBy(x,y)（仅IE支持）每单击一次扩大宽度跟高度

* resizeTo() 把窗口的大小调整到指定的宽度和高度(仅IE支持) 固定

* **scrollBy() 按照指定的像素值来滚动内容 scrollBy(x,y) 滚动了多少像素**

* **scrollTo() 按照指定的像素值滚到到此为止   window.scrollTo(0,0)**

* **setTimeout() 延迟器 在指定的毫秒数后调用函数或计算表达式**   **setTimeout(函数名，ms毫秒) 只能出来一次**  

  **网页全部加载完才会开始执行setTimeout()里面的内容**    **单线程**   配合clearTimeout()

* **clearTimeout() 取消由setTimeout()方法设置的timeout   清除的是变量**

  ```javascript
  					/*setTimeout*/
  					/*clearTimeout*/
  var j=setTimeout(function(){
  	alert("Hello");
  },1000);
  clearTimeout(j);
  					/*setInterval*/
  					/*clearInterval*/
  var j=setInterval(function(){
      alert("Hello");
  },5000);
  function toStop(){
      clearInterval(j);
  }
  ```

  ```javascript
  for(var i=0;i<5;i++){		/*0 1 2 3 4 5 5 5 5 5*/ /*页面内容全部加载完毕后才会加载setTimeout由于循环完的i变成5所以setTimeout中的console.log输出五次5*/
  	console.log(i);
  	setTimeout(function(){
  		console.log(i)
  	},0);
  }
  ```

  ```javascript
  console.log(1);				/*1 3 2 4*/
  setTimeout(function(){
  	console.log(2);
  },0);
  console.log(3);
  setTimeout(function(){
  	console.log(4);
  },1000);
  ```

  ```javascript
  <form action="#" name="myForm">
      <input type="buttom" value="发送验证码" name="btn" onclick="countDown()">
  </form>
  
  var i=10,j;
  function countDown(){
  	if(i<=0){
  		doucment.myForm.btn.disabled=false;
  		document.myForm.btn.value="重新发送";
          i=10;						/*如果不清理的话i会始终往下减1*/
          clearTimeout(j);
  	}else{
          i--;
          document.myForm.btn.disabled=true;
          document.myForm.btn.value="还剩"+i+"s";
          j=setTimeout(countDown,1000);
      }
  }
  ```

* setInterval() 按照指定的周期(以毫秒计)来调用函数或计算表达式   setInterval(函数名，ms) 配合clearInterval使用

  ```javascript
  /*在函数里面需要先清理再定时
  settimeout()与setInterval()的区别：settimeout是只出来一次  setInterval()一直出来
  ```

  ```javascript
  setInterval(function(){
      var da=new Date();
      var h=da.getHours();
      var m=da.getMinutes();
      var s=da.getSeconds();
      document.myForm.f1.value=(h+":"+m+":"+s);
  },1000);
  ```

  

* clearInterval() 取消由setInterval()设置的timeout 清除的是变量

## 9.3 Navigator对象--属性

* cookieEnabled 返回指明浏览器中是否启用cookie的布尔值 true/false

  ```javascript
  console.log(navigator.cookieEnabled);
  ```

* userAgent 返回由客户机发送服务器的useragent头部的值   返回浏览器的名字/版本号/移动端的系统/手机型号

  ```
  console.log(navigator.userAgent);
  ```

  ```javascript
  var user=navigator.userAgent.toLowerCase();
  if(user.indexOf("chorme")!=-1){
  	console.log("谷歌");
  }else if(user.indexOf("ie")!=-1){
  	console.log("IE");
  }else if(user.indexOf("firefox")!=-1){
  	console.log("火狐");
  }else if(user.indexOf("opera")!=-1){
  	console.log("欧朋");
  }else{
  	console.log("没有找到匹配的浏览器");
  }
  ```


## 9.4 Navigator对象--方法

javaEnabled()规定浏览器是否启用Java

```
console.log(navigator.javaEnabled());
```

6个宽高总结在一起 screen window

浏览器内核

封装

## 9.5 Screen对象--属性

* availHeight返回显示屏幕的高度(除Windows任务栏之外)
* availWidth返回显示屏幕的宽度(除Windows任务栏之外)
* height返回屏幕的高度 包含任务栏
* width返回屏幕的宽度 包含任务栏

```javascript
/*单击按钮在页面中间显示*/

<form action="#">
     <input type="button" value="点击" onclick="test()" class="bt">
</form>

function test(eq,hh,wid,hei){
    var t=(screen.height-hei)/2;
    var l=(screen.width-wid)/2;
    var wid=300;
    var hei=200;
    window.open(eq,hh,"width="+wid+",height="+hei+",top="+t+",left="+l);
}
test('equipment.html','hh',300,300);
```

## 9.6 History对象--属性

包含用户在浏览器窗口中访问过的URL

length 返回浏览器历史列表中的URL数量(当前页面也算--必须点击过才算一个浏览量)

## 9.7 History对象--方法

* back() 加载history中的前一个URL

  ```
  history.back();
  ```

* forword() 加载history中的后一个URL

  ```
  history.forward();
  ```

* go() 正值是前进 负值是后退

## 9.8 Localtion 对象--属性

获取当前URL的信息(javascript里面管理地址栏的内置对象)

* **hash[打开控制台演示]设置或返回从#开始后面的内容  获取--哈希值

* host 设置或返回主机名或端口号

* hostname 设置或返回当前URL的主机名

* **href 返回一个完整的URL

  ```javascript
  function test(){
  	location.href="product.html";
  }
  ```

* pathname 返回URI部分
* port 设置或返回当前URL的端口号
* protocol 设置或返回当前的URL协议
* **search 返回从?后面开始的内容  明文提交表单时

```javascript
/*截取从明文提交的用户名与密码*/
/*第一种方法*/
function test(){
var str=location.search;
console.log(str);
var strNew=(str.substr(1));//去掉?
console.log(strNew);
var arr=(strNew.split("&"));
console.log(arr[0]);
console.log(arr[1]);
console.log(arr[0].substr(arr[0].indexOf("=")+1));
console.log(arr[1].substr(arr[1].indexOf("=")+1));
}
test();
/*第二种方法*/
var str=location.search;	/*获取用户名和密码所对应的值，所以需要把用户名和密码分开,所以使用split这个方法进行分割，将他分割成一个字符串数组，下标为arr[0]和arr[1]*/
var strNew=str.substr(1);
var arr=strNew.split("&");	/*分割为"username=admin", "pwd=456"*/
for(var i=0;i<arr.length;i++){	/*将用户名和密码分割开后需要获取后面的值，由于=连接前后，所以继续使用split这个方法进行分割，分割成*/
    var arrNew=arr[i].split("=");	/*arr[0]:username=admin arr[1]:pwd=456*/
    console.log(arrNew[1]);			/*arr[0]---arrNew[0]:username arrNew[1]:admin*/
}								/*arr[1]---arrNew[0]:pwd arrNew[1]:456*/
	    var arrNew=arr[0].split("=");//将arr[0]再次分割为一个字符串数组 =前为arrNew[0]，=后为arrNew[1]
        console.log(arrNew[1]);
        var arrNew=arr[1].split("=");
        console.log(arrNew[1]);//将arr[1]分割为一个字符串数组=前为arrNew[0]，=后为arrNew[1]
```

## 9.9 Location 对象--方法

* assign("http://www.baidu.com"); **能回到原来的页面** 跳转链接 不放封装时自动跳转
* reload();刷新 括号里面为空
* ***replace("http://www.baidu.com") 用新的文档替换当前文档 **找不到原来的页面**

## 9.10 Frames对象--属性

**window.frames  获取的是所有的框架 是一个数组 frames[0]为第一个 从上往下从左往右获取框架**

```javascript
for(var i=0;i<window.frames.length;i++){
	window.frames[i].document.write("这是第"+(i+1)+"个框架");/*由于数组下标为0，不能从第0个框架开始所以i要+1*/
}/*再次强调window.frames是一个数组 所以进行遍历输出*/
```

BOM对象：

* window:innerWidth、innerHeight 三个弹出框及区别
* open这个方法 
* scrollBy、scrollTo(返回顶部)
* set(clear)Timeout延迟器、set(clear)Interval定时器  使用的时候必须使用clear否则内存泄漏 占用内存
* navigator：userAgent 判断内核/浏览器/
* screen:availHeight、availWidth、width、height
* histrory:go() 正值前进、负值后退
* location：获取的是和url相关的信息
* hash、href(常用的是跳转页面)、search
* replace

## 9.11 Document对象--DOM对象

document对象代表当前文档

从<!doctype html>到</html>都是document

# 第十章 DOM对象

- DOM特点：可以对整个HTML文档进行新建、添加、更新、删除等操作。
- 兼容性好
- 通过DOM操纵HTML、XHTML、XML文档

## 10.1 DOM树

```
文档--根元素:<html>--<head>--<title>--文本:"文档标题"
				--<body>--<body>--元素:<a>（属性：href）--------------元素:<h1>
								----文本:"我的链接"	 ---文本:"我的链接"
```

1. 整个文档是一个文档节点
2. 每个HTML标签是一个元素节点
3. 包含在HTML元素中的文本是文本节点
4. 每一个HTML属性是一个属性节点
5. 注释属于注释节点

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>DOM说明</title>
</head>
<body>
    <h1>DOM Lesson one</h1>
    <p>Hello world!</p>
</body>
</html>
<!--
1.除文档节点之外的每个节点都有父节点。例如：<head>和<body>的父节点是<html>节点，文本节点"Hello world!"的父节点是<p>大部分节点都有子节点。例如<head>节点有一个子节点<title>节点。title也有一个子节点:文本节点"DOM说明"
2.当节点分享同一个父节点时，他们就是兄弟(同级节点)。例如<h1>和<p>就是同辈，因为他们的父节点均是<body>节点
3.节点也可以拥有后代，后代指某个节点的所有子节点，或者这些子节点的子节点，以此类推，例如，所有文本节点都是<html>节点的后代，而第一个文本节点是<head>节点的后代。
4.节点也可以拥有祖先。祖先是某个节点的父节点，或者父节点的父节点，以此类推，比如，所有的文本节点都可以把<html>系欸但作为先辈节点
-->
```

## 10.2 Document对象获得文档元素

一共五种方法

### 10.2.1 通过ID值找元素document.getElementById(id)

document.getElementById(id)只找一个

```javascript
document.getElementById("d2").className="aa";
/*加类别选择器 前面是对象：className=“aa” 给id为d2的div加上类别选择器*/
```

### 10.2.2 通过name属性找元素(数组)document.getElementsByname(name)

```javascript
var d1=document.getElementByname("d1");
for(var i=0;i<d1.length;i++){
	d1[i].className="aa";
}
/*document.getElementsByName数组遍历时只能用for()遍历，否则会多出很多属性*/
```

不同的元素之间可以共用一个属性 例如：sex  getElements有s的找的就是数组 没s的找的是元素 

classname操作的是具体的对象 而getElementsByName是数组

Byname、byTagName获取的时候只能用for()遍历，否则会多出来很多属性

### 10.2.3 通过 标记名(数组)document.getElementsByTagName(tagname)

```javascript
var d=document.getElementsByTagName("div");
for(var i=0;i<d.length;i++){
	d[i].className="aa";
}
```

```javascript
<div name="d1">div1</div>
<div id="d2">
	<div>div4</div>
</div>
<div name="d1"></div>
document.getElementById("d2").getElementsByTagName("div")[0].className="aa";/**/
/*给id为d2下的标记名为div加className   因为getElementsByTagName是一个数组所以里面的内容需要用下标表示因为是第一个div所以下标为[0]*/
```

### 10.2.4 类别document.getElementsByClassName(数组)--不推荐使用

可以找到对象 但是加类别选择器时只能改第一个

```javascript
/*不推荐使用 有局限性*/
var d=document.getElementsByClassName("d1");
for(var i=0;i<d.length;i++){
	d[i].className="aa";
}
```

### 10.2.5 通过name名

document.myForm.username.value; 通过name名 

弊端：如果外面嵌套一个标签都无法找到 

## 10.3 Document对象节点信息

### 1.节点名称

* 元素节点的nodeName是标签的名称
* 属性节点的nodeName是属性的名称(获取属性节点对象名.Attributes[下标])
* 文本节点的nodeName永远都是#text
* 文档节点的nodeName永远是#document

### 2.nodeValue节点值

* 对于文本节点，nodeValue属性包含文本
* 对于属性节点，nodeValue属性包含属性值

nodeValue属性对于文档节点和元素节点是不可用的(null)

### 3.节点类型

* 元素  1
* 属性  2
* 文本  3
* 注释  8
* 文档  9

## 10.4 Document对象操纵节点

### 10.4.1 创建节点

1.createElement("标记")--创建一个**元素**节点，想创建哪个标记就在里面写哪个  创建一个新的标记

```javascript
var p1=document.createElement("p")
```

2.createTextNode("文本")创建一个**文本**节点 里面写什么就显示什么

```javascript
var t1=document.createTextNode("好好学习，天天向上");
```

### 10.4.2 添加节点

#### appendChild(node)--移动到后面

对象（父元素）.apppendChild(node（要添加的对象）) 在指定元素内部的**后面**添加 

```javascript
d1.appendChild(p1);
d1.appendChild(t1);
```

没有：如果原本没有就会直接添加到父元素的后面

已有：如果是原本有的 那么就把他从原来的为止移动到父元素对象的后面

#### insertBefore(要添加或移动的节点，参考节点)--移动到前面**

对象(父元素 添加到谁).insertBefore(要添加或要移动的节点，参考节点【谁前面】)

有的话就是移动，没有就是创建

```javascript
var d1=document.getElementById("d1");
var s2=document.getElementById("s2");
var t1=document.createTextNode("我是新创建的文本");
var p2=document.getElementById("p2");
d1.insertBefore(t1,s2);
```

### 10.4.3 删除节点

removeChild(node);

父元素.removeChild(node【要删除的节点是谁】)删除节点   无法删除文本节点 因为文本节点没有名字  只能删除元素节点

```javascript
var d1=document.getElementById("d1");
var s2=document.getElementById("s2");
d1.removeChild(s2);
```

### 10.4.4 复制节点

cloneNode(true)--深拷贝 不仅复制标记还复制里面的内容

cloneNode(false)--浅拷贝 复制的只有里面的标记

d1.appendChild.想要复制的节点.复制节点cloneNode(true)

```javascript
var d1=document.getElementById("d1");
var s2=document.getElementById("s2");
var p2=document.getElementById("p2");
d1.appendChild(p2.cloneNode(true)); 
```

### 10.4.5 替换节点

父.replaceChild(新，换)	 只要替换了 原来的元素就没有了

```html
<div id="d1">
    <span>span1</span>
    <span id="s2">span2</span>
</div>
<p id="p2">我是p2</p>
<span>span3</span>
```

```javascript
var d1=document.getElementById("d1");
var s2=document.getElementById("s2");
var p2=document.getElementById("p2");
d1.replaceChild(p2,s2);
```

### 10.4.6 判断节点是否有子节点

hasChildNodes判断是否包含有子节点 布尔值 在控制台打印   空格/换行也是节点 有文本也算

```javascript
var d1=document.getElementById("d1");
var s2=document.getElementById("s2");
var p2=document.getElementById("p2");
d1.hasChildNodes(p2);
```

### 10.4.7 是否包含某节点

父.contains(p2) 判断是否包含某个节点  布尔值  只能判断节点

```javascript
var d1=document.getElementById("d1");
var s2=document.getElementById("s2");
var p2=document.getElementById("p2");
d1.contains(p2);
```

### 10.4.8 更改为父节点

更改为父节点   parentNode属性   找的是父元素 更改对象为当前节点的父节点

```html
<div id="d1">
    <span>span1</span>
    <span id="s2">span2</span>
</div>
<p id="p2">p2</p>
```

```javascript
var s2=document.getElementById("s2");
s2.parentNode.className="aa";
```

### this指向的对象是window--面试题

* this 指向的是window
* Js基于window对象，window这个对象是js中的顶级对象，this代表的是当前对象，直接打印this的话代表的是一个对象，所以打印this出来的必定是window对象 因为没有其他的对象，如果把this放在一个函数中，那么this代表的是window
* 只有new出来的代表的是这个对象，但是如果没有New的话指向的还是window

### 10.4.9 父元素下的第一个子节点

firstChild 找的是第一个子节点 前面不能有空格，否则获取的是文本节点

### 10.4.10 父元素下的最后一个子节点

lastChild 找的是最后一个子节点  前面也不能有空格，否则获取的还是文本节点

### 二级菜单

```html
<ul id="nav"><li onmouseover="shows()" onmouseout="hides()"> 
    <a href="#">产品介绍</a>	<!--onmouseover鼠标划入调用shows方法 onmouseout鼠标划出调用hides方法-->
    <ul>
        <li><a href="#">脑白金</a></li>
        <li><a href="#">六个核桃</a></li>
        <li><a href="#">脑黄金</a></li>
    </ul></li>	<!--此处ul与li之间不可有空格或者回车否则获取的值为文本节点-->
</ul>
```

```javascript
function shows(){  /*找ID为nav下的第一个子元素下的最后一个子元素给他加类别选择器aa*/
    document.getElementById("nav").firstChild.lastChild.className="aa";
}			/*鼠标划入时给他加上类别选择器aa*/
function hides(){/*找ID为nav下的第一个子元素下的最后一个子元素给他加类别选择器为空*/
    document.getElementById("nav").firstChild.lastChild.className="";
}			/*鼠标划出的时候不给他加类别选择器*/
```

```css
	ul{
        margin:0;
        padding:0;
        list-style-type:none;
    }
    ul>li{
        width:120px;

    }
    ul>li>a{
        display:block;
        width:120px;
        height:30px;
        text-align:center;
        line-height:30px;
        background-color:#362984;
        color:#fff;
        text-decoration: none;
    }
    #nav ul{
        display:none;
    }
    #nav .aa{
        display:block;
    }
```

通过父元素找的只有在范围里的才能被找到 ，如果是document找的将是整个文档，按照整体顺序下标来查找

### 10.4.11 子节点的集合

* childNodes **包含有文本节点(**下标从0开始)

  ```javascript
  var d1=document.getElementById("d1")
  d1.children[0].className="aa";
  for(var i=0;i<d1.children.length;i++){
  	d1.children[i].className="aa";
  }
  ```

* children **不包含文本节点只有元素节点**(下标从0开始)

### 10.4.12 兄弟节点

* nextSibling 下一个兄弟 包含文本节点

  ```javascript
  var d1=document.getElementById("d1");
  var p2=document.getElementById("p2");
  p2.nextSibling.className="aa";
  ```

* previousSibling 上一个兄弟 包含文本节点

  ```javascript
  var d1=document.getElementById("d1");
  var p2=document.getElementById("p2");
  p2.previousSibling.className="aa";
  ```

* previousElemntSibling 上一个兄弟节点 不包含文本节点

  ```javascript
  var d1=document.getElementById("d1");
  var p2=document.getElementById("p2");
  p2.previousElementSibling.className="aa";
  ```

* nextElementSibling 下一个兄弟 不包含文本节点

  ```javascript
  var d1=document.getElementById("d1");
  var p2=document.getElementById("p2");
  p2.nextElementSibling.className="aa";
  ```

## 10.5 元素中的属性设置

* getAttribute("属性名")获得节点属性中的值

  ```java
  var im=document.getElemntsByTagName("img")[0];
  console.log(im.getAttribute("src"));
  ```

* setAttribute("属性名","值") 设置节点属性 一次只能设置一个 没有此属性的时候还可以用它设置

  还可以用它设置class以及ID 他们都是属性

  ```javascript
  var im=document.getElemntsByTagName("img")[0];
  console.log(im.getAttribute("src"));
  im.setAttribute("src","../img/2.jpg");
  im.removeAttribute("width");
  ```

  ```javascript
  /*没有属性的时候setAttribute还可以创建属性*/
  <img src="../img/1.jpg">
  .aa{
      border:#000 solid 2px
  }
  var im=document.getElemntsByTagName("img")[0];
  console.log(im.getAttribute("src"));
  im.setAttribute("class","aa");
  ```

* removeAttribute("属性值") 删除节点属性

## 10.6 样式设置

* html属性怎么写，js就怎么写 document.name.属性

  ```javascript
  var im=document.getElementsByTagName("img")[0];
  console.log(im.src);/*找对象的方式使用的是找form表单的方式 找的是name所以在js中没有值*/
  im.src="../img/2.jpg";  /*注意路径*/
  ```

* 对象.style.属性**(添加到行内样式**，css样式去掉-，必须符合国际命名【backgroundColor】) 只能设置一个

  ```javascript
  var im=document.getElemntsByTagName("img")[0];
  im.style.width="200px";
  im.style.border="1px #000 solid";
  im.style.backgroundColor="#f00";/*"-"需要去掉使用驼峰命名法，每次只能设置一个*/
  ```

* 对象.style.cssText属性(**行内样式**，可以一次添加多个样式);

  ```javascript
  var im=document.getElemntsByTagName("img")[0];
  im.style.cssText="width:200px;height:200px;background-color:#f00";
  ```

* className属性(应用类选择器class=类名);

  ```javascript
  var im=document.getElemntsByTagName("img")[0];
  im.className="aa";
  ```

例题：点击按钮，图片变换

```html
<button onclick="changeImg(1)">1</button>
<button onclick="changeImg(2)">2</button>
<button onclick="changeImg(3)">3</button>
<button onclick="changeImg(4)">4</button>
<button onclick="changeImg(5)">5</button>
<img src="../img/1.jpg" name="im">
```

```javascript
function changeImg(i){
    document.im.src="../img/"+i+".jpg";
}
```

### 播放图片

```javascript
/*每隔5秒就随机播放一张图片*/
setInterval(function(){
	var i=Math.ceil(Math.random()*18);
	document.im.src="../img/"+i+".jpg";
},5000)
```

```javascript
/*每隔5秒就按照顺序播放一张图片*/
var i=1;	/*设置全局变量否则不会变动*/
setInterval(function(){
    document.im.src="../img/"+i+".jpg";
    i++;
    if(i==19){
        i=1;
    }
},5000)
```

```html
<!--按照顺序播放图片鼠标划入停止播放，鼠标划出播放继续，点击按钮图片变换-->
<button onclick="changeImg(1)">1</button>
<button onclick="changeImg(2)">2</button>
<button onclick="changeImg(3)">3</button>
<button onclick="changeImg(4)">4</button>
<button onclick="changeImg(5)">5</button>
<img src="../img/1.jpg" name="im" onmouseover="cle()" onmouseout="st()">
```

```javascript
var i=1;
function scrol(){
    document.im.src="../img/"+i+".jpg";
    i++;
    if(i==19){
        i=1;
    }
}
var j=setInterval(scrol,5000)
function cle(){
    clearInterval(j);/*清空*/
}
function st(){
    j=setInterval(scrol,5000);/*重新给值*/
}
```

### 找a其他的兄弟

```html
<div>
    <p></p>
    <h1></h1>
    <h2></h2>
    <a href="#" id="a1">a</a>
    <span>span1</span>
</div>
```

```javascript
var a1=document.getElementById("a1");
var ch=a1.parentNode.children;
for(var i=0;i<ch.length;i++){
	if(ch[i]!=a1){
		alert(ch[i]);
	}
}
/*找到a1,然后a1的父元素下的子元素,子元素是一个数组所以要遍历输出,判断输出数组中不等于a1的标签*/
```

### 图片轮播、点击从当前开始轮播

```html
<div id="banner">
    <img src="../img/1.jpg" id="ima">
    <span onclick="showImage(1)">1</span>
    <span onclick="showImage(2)">2</span>
    <span onclick="showImage(3)">3</span>
    <span onclick="showImage(4)">4</span>
</div>
```

```javascript
var ima=document.getElementById("ima");
var i=19;/*18*/
function scrollImage(){
	ima.src="../img/"+i+".jpg";
	i++;
	if(i==24){	 /*23*/
		i=19;	/*18*/
	}
}
var j=setInterval(scrollImage,5000);
function showImage(a){/*把a当做形参，从方法中获取实参*/
	ima.src="../img/"+a+".jpg";
	i=a;/*将a的值赋给i，i是进行轮播的值*/
}
```

### 把?后面的值获取出来放到p里面

```javascript
var url="?username=admin&pwd=123456";
var urlNew=url.subsrt(1);
var arr=urlNew.split("&");
for(var i=0;i<arr.length;i++){
	p=document.createElement("p");
	p.innerHTML=arr[i];
	document.getElementById("banner").appendChild(p);
}
```

## 10.7 文档节点处理

* innerText属性 用文本替换掉当前元素里面的子节点或文本节点 

  ```javascript
  在banner这个容器中有一个文本元素
  document.getElementById("banner").innerText="我是文本";
  ```

* innerHTML属性 用某一个元素节点替换当前的子节点

  ```javascript
  /*可以把内容解析为HTML的代码*/
  document.getElementById("banner").innerHTML="<p>我是文本</p>";
  ```

  ##### innerHTML与document.write的区别：

  **innerHTML:是改变某一个块中的内容**

  **document.write():刷新的是整个页面**

* outerText属性 firefox不支持

  ```javascript
  /*整个替换掉外面的容器*/
  document.getElementById("banner").outerText="我是文本"; /*banner这个id的容器将消失只剩下outerText中写的文本*/
  ```

* outerHTML属性 替换当前节点

  ```javascript
  /*容器将整个被替换掉，只剩下outerHTML中写的内容*/
  document.getElementById("banner").outerHTML="<div>我要</div>";
  ```

## 总结

1. 什么是DOM：文档对象
2. 找对象的方法：id、name、TagName、className(只能操作一次，但是都能找到)、表单form
3. 创建对象的方法：createTextNode(文本节点)、createElement(元素节点)
4. 添加节点方法：appendChild、对.insertBefore(新节点，参考节点【谁的前面】)
5. 删除(removeChild)、替换(replaceChild)、判断子节点(hasChildNodes)、判断某个指定节点(contains)
6. 父亲、第一个、最后一个、兄弟、孩子
7. 复制节点：cloneNode：深拷贝、浅拷贝

# 第十一章 事件驱动

## 11.1 事件驱动概述

事件：窗体、对象、鼠标、键盘动作都成为事件

## 11.2 事件绑定方式

​		主要有三种

* 放在HTML中，行内绑定(不建议)：无法实现标记和和动作分离

* 对象名.事件名=function(){语句;语句;}

  先找对象再给加事件

  ```javascript
  document.getElementById("banner").onclick=function(){
  	alert("好好学习，天天向上");
  }
  ```

  ```javascript
  var d=document.getElementsByTagName("div");/*遍历数组d,使用对象名.事件名=function(){}*/
  for(var i=0;i<d.length;i++){
  	d[i].onclick=function(){
  		alert("好好学习，天天向上");
  	}
  }
  ```

  ```javascript
  var d=document.getElementsByTagName("div");/*遍历数组d,使用对象名.事件名=function(){},this的意思代指当前遍历的这个数组的下标i,即指谁就是谁,相当于指针*/
  for(var i=0;i<d.length;i++){
  	d[i].onclick=function(){
  		this.innerHTML="好好学习，天天向上";
  	}
  }
  /*1. 直接在js中写this,那么this 指向的是window
  2. 在哪个操作对象下面写this,那么this指向的就是这个操作对象*/
  ```

* 对象名.addEventListener("事件名",函数名,捕获过程true/冒泡过程false【默认是false】)  **前面一点不能有on**

  说明：IE6/7/8的兼容方式是:attachEvent("on事件名",函数)  移动端的绑定事件方式也是addEventListener

  ```javascript
  var d=document.getElementsByTagName("div")[0];
  function test(){
  	alert("hello");
  }
  d.addEventListener("click",test,false);
  ```

```javascript
/*判断兼容性*/
if(d.addEventListener){
    d.addEventListener("click",test,false);
}else{
    d.attachEvent("onclick",test);
}
```

```javascript
function addEvent(elem,evtType,func){
	if(elem&&typeof(elem)=="object"){
		if(elem.addEventListener){
			elem.addEventListener(evtType,func,false);
		}else{
			elem["on"+evtType]=func;
		}
	}
}//1.自动刷新事件2.验证码
```

### this的指向问题

1. 直接在js中写this,那么this 指向的是window
2. 在哪个操作对象下面写this,那么this指向的就是这个操作对象

* 作业：把？后面的值获取出来放到p里面

* 图片划入放大划出变小

* 上课讲到的所有的例子

* 欢迎光临 迎光临欢 光临欢迎 临欢迎光 把第一个字符放在最后

  ```javascript
  /*第一种方法*/
  var str="欢迎光临";
  setInterval(function(){
  	str=str.substr(1)+str.substr(0,1);
  	document.getElementsByTagName("span")[0].innerHTML=str;/*将最后的值赋给span*/
  },2000)
  /*将字存放在字符串中，每次都是把第一个字符放在最后因此使用截取substr把后三个字截取出来连接上第一个，最后将结果放在span中找到span这个对象.innerHTML是放在span标签中*/
  ```

  ```javascript
  /*第二种方法*/
  var d=document.getElementsByTagName("div")[0];
  setInterval(function(){
  	ch=d.children;
  	d.appendChild(ch[0]);
  },2000)
  /*找到div，然后创建一个数组把div下的子元素都存放进去，将ch数组中的第一个元素拿出来appenChild放在div的最后面*/
  ```

## 11.3 事件类型

### 11.3.1 onload--加载完成 如果不想把script放在下面就加上onload 

1. 放在js中 window.onload=function(){"js代码"}

2. 支持该事件的对象image,window

3. 支持该事件的标记body,fra?>me,frameset,iframe,img,link,script

   ```javascript
   window.onload=function(){
   	var d=document.getElementById("d1");
   	alert(d.innerHTML);
   }
   ```

### 11.3.2 onresize--改变浏览器尺寸的时候调用，窗口的放大缩小

1. 支持他的对象有window

2. window.onresize=function(){}

   ```
   window.onresize=function(){
   	alert("你缩放了当前页面");
   }
   ```

### 11.3.3 onscroll--滚动条滚动

1. 支持该事件的对象window

2. window.onscroll=function(){}

   ```
   window.onscroll=function(){
   	alert("你滚了");
   }
   ```

### 11.3.4 键盘鼠标

单击事件--onclick

双击事件--ondbclick

卸载文件--onunload

鼠标左键按下--onmousedown

鼠标左键抬起--onmouseup

鼠标移动--onmousemove

获取鼠标--onmouseover

失去鼠标--onmouseout

键盘按下--onkeydown

键盘抬起--onkeyup

按键盘--onkeypress

```javascript
var sp=document.getElementById("sp");
var spt=document.getElementById("spt");
sp.onkeyup=function(){
	if(this.value.length>=6 && this.value.length<=12){/*这里的this可以直接写sp因为不是指定的某一个*/
		spt.innerHTML="输入正确";
         spt.className="success";
	}else{
		spt.innerHTML="请输入长度在6到12个字符之间";
         spt.className="error";
	}
}
/*找到id名对应的容器，当键盘抬起的时候调用这个方法：当里面的值大于等于6小于等于12的时候执行输入正确这条命令，否则的话执行报错*/
```

```html
<input type="text" id="sp"><span id="spt"></span>
```

### 11.3.5 二级菜单

```javascript
var l=document.getElementById("nav").children[0].children;
for(var i=0;i<l.length;i++){
	l[i].onmouseover=function(){
		this.children[1].className="aa";/*children[1]的意思是他是li下的第二个子元素，给他加类选择器*/
	}
	l[i].onmouseout=function(){
		this.children[1].className="";/*鼠标划出的时候不加类别选择器*/
	}
}
/*因为i已经等于最大值了回不去所以必须使用this 找的是原来i的值 而不是 现在i的值，有关系的情况下用this*/
```

```javascript
/*传参数*/
function navbar(elementId,cname){
    var l=document.getElementById(elementId).children[0].children;
	for(var i=0;i<l.length;i++){
	l[i].onmouseover=function(){
		this.children[1].className=cname;
	}
	l[i].onmouseout=function(){
		this.children[1].className="";
	}
}
}
navbar("nav","aa");
```

```html
<div id="nav">
    <ul>
        <li>
        	<a href="#">首页</a>
        </li>
        <li>
        	<a href="#">关于我们</a>
            <ul>
                <li><a href="">关于公司</a></li>
                <li><a href="">关于产品</a></li>
                <li><a href="">关于售后</a></li>
            </ul>
        </li>
        <li>
        	<a href="#">产品介绍</a>
            <ul>
                <li><a href="">烤冷面</a></li>
                <li><a href="">烤面筋</a></li>
                <li><a href="">手抓饼</a></li>
                <li><a href="">土豆饼</a></li>
            </ul>
        </li>
    </ul>
</div>
```

```css
#nav ul{
	list-style-type:none;
	margin:0;
	padding:0;
}
#nav>ul>li{
	float:left;
}
#nav ul li a{
	dispaly:block;
	width:120px;
	height:40px;
	text-align:center;
	line-height:40px;
	background-color:#888555;
	text-decoration:none;
}
#nav ul li ul{
	display:none;
}
#nav ul li ul a{
	background-color:#687623;
}
#nav ul li .aa{
	display:block;
}
```

### 11.3.6 选项卡

```html
<div id="content">
            <button>1</button>
            <button>2</button>
            <button>3</button>
            <button>4</button>
            <div style="display:block;">项目一</div>
            <div>项目二</div>
            <div>项目三</div>
            <div>项目四</div>
</div>
```

```javascript
var con=document.getElementById("content");
var btn=con.getElementsByTagName("button");
var di=con.getElementsByTagName("div");
for(var i=0;i<btn.length;i++){
	btn[i].index=i;/*index相当于是一个变量，把i的值赋给btn[i]下的index变量*/
    /*btn[i].a=i*/
	btn[i].onclick=function(){
		for(var j=0;j<di.length;j++){
			di[j].style.display="none";/*遍历给div全部设置隐藏*/
		}
		di[this.index].style.display="block";/*this.index指的是当前btn[i]中的下标*/
        /*di[this.a].style.display="block"*/
	}
}
/*属性就是变量，方法就是函数*/
/*因为i已经等于最大值了回不去所以必须使用this 找的是原来i的值 而不是 现在i的值，有关系的情况下用this*/
```

因为i已经等于最大值了回不去所以必须使用this 找的是原来i的值 而不是 现在i的值，有关系的情况下用this 

### 11.3.7 表单事件

* 改变事件onchange 值改变的情况下失去焦点后会触发 

  ```javascript
  document.getElementById("username").onchange=function(){
  	console.log(this.value);
  }
  ```

* 选中事件onselect  用于文本选中的情况下

  ```javascript
  document.getElementById("username").onselect=function(){
  	console.log(this.value);
  }
  ```

* 获得焦点事件onfocus 常用于用户名密码的未输入后的提示

  1. 对象名.onkeyup=test;    这种方式无法传参

  2. 但是如果单独写会自动的调用这个函数test()  这种方式可以传参

* 失去焦点onblur

* 重置事件onreset  只有form标签才能用

* 提交事件onsubmit   只有form标签才能用  

  ```javascript
  document.getElementById("username").onkeyup=function(){
  	test(this.value,this.nextElementSibling);
  }
  document.getElementById("pwd").onkeyup=function(){
  	test(this.value,this.nextElementSibling);
  }
  function test(argumentsU,argumentsA){
  	if(argumentsU.length>=6 && argumentsU.length<=12){
  		argumentsA.innerHTML="输入正确";
  	}else{
  		argumentsA.innerHTML="请输入6-12个字符之间";
  	}
  }
  ```

  ```html
  <input type="text" id="username"><span id="usera"></span>
  <input type="password" id="pwd"><span id="pwda"></span>
  ```

  ```javascript
  document.getElementById("username").onkeyup=function(){
  	test(this.value);
  }
  function test(argumentsU){
  	if(argumentsU.length>=6 && argumentsU.length<=12){
  		document.getElementById("usera").innerHTML="输入正确";
  	}else{
  		document.getElementsById("usera").innerHTML="请输入6-12个字符之间";
  	}
  }
  ```

  ```html
  <input type="text" id="username"><span id="usera"></span>
  ```

### 11.3.8 表单验证提交

```html
<form onsubmit="return sub()"></form>
```

```javascript
/*当内容填写正确且不为空的时候允许提交，反之不允许*/
var a=false,b=false,c=false;/*需要借助变量一开始给变量赋值为false的好处在于如果执行了输入正确这条语句则代码一定是正确的然后再给这个变量赋值为true，确定他的准确性*/
document.getElementById("pwd2").onblur=function(){
	var pwd=document.getElementById("pwd");
	if(this.value==pwd.value){/*此处是对比两次密码是否一致*/
		this.nextElementSibling.innerHTML="输入正确";
         b=true;/*如果一致给这个变量赋值为true*/
	}else{
		this.nextElementSibling.innerHTML="两次密码输入不一致";
	}
}

function sub(){/*本方法的作用为判断变量的值，如果任何一个内容填写的错误返回的都是false则无法提交，反之则提交*/
    if(a==false || b==false || c==false || d=false){
        return false;
    }else{
        return true;
    }
}
```

## 11.4 事件对象

事件本身也是一个对象 成为事件对象 由系统自动创建的  事件对象存在于回调函数的参数

对象名.事件名=function(event【e】){} 或者  window.event

事件对象局限于当前这个事件当中

兼容写法:e=window.event || e;

```javascript
var d1=document.getElementById("d1");
d1.onclick=function(e){
	this.innerHTML="你单击了这个div";
	e = window.event || e;
}
```

### 11.4.1 事件对象的属性

* 标准方式:(chrome/firefox)

  button鼠标左键、中键、右键

  0左键  1中键  2右键

  ```javascript
  var d1=document.getElementById("d1");
  d1.onclick=function(e){
  	this.innerHTML="你单击了这个div";
  	e = window.event || e;
  	console.log(e.button);
  }
  ```

* IE拥有不同的参数:

  1左键  4中键  2右键

* target 返回触发当前事件的对象

  说明:IE6/7/8浏览器写法srcElement

  ```javascript
  document.getElementById("d1").onkeyup=function(e){
  	e = e || window.event;
  	console.log(e.target);
  }
  ```

* type 返回当前事件的名称

* screenX 鼠标指针的**屏幕**水平坐标

* screenY 鼠标指针的**屏幕**垂直坐标

* clientX 鼠标指针相对于**浏览器窗口**的水平坐标，不包含左右侧边栏和滚动条

* clientY 鼠标指针相对于**浏览器窗口**的垂直坐标，不包含左右侧边栏和滚动条  

  IE中写法X Y firefox写法pageX pageY

* offsetX 鼠标相对于**当前区域**的水平坐标 firefox不支持 IE和Chorme支持 

  **兼容写法:e.clientX-this.offsetLeft**

  ```javascript
  console.log(e.clientX-this.offsetLeft)/console.log(e.clientY-this.offsetTop)
  /*其实就是margin值*/
  document.getElementById("d1").onclick=function(e){
      e = e || window.event;
      console.log(e.clientX-this.offsetLeft);
  }
  ```

* offsetY 鼠标相对于**当前区域**的垂直坐标 firefox不支持 IE和Chorme支持

### 11.4.2 事件对象的方法

* **preventDefault() 标准写法，阻止默认动作(事件)**

  说明:IE兼容写法returnValue属性=false

  ```javascript
  document.getElementsByTagName("a")[0].onclick=function(e){
  	e = e || window.event;
  	e.preventDefault();
  }
  ```

* **stopPropagation()标准写法**

  阻止触发3的时候，是3引起，谁触发给谁加

  event.stopPropagation();

  说明:IE兼容写法cancelBubble=true;

  ```javascript
  document.getElementById("d1").onclick=function(){
  	alert("你单机了div1");
  }
  document.getElementById("d2").onclick=function(){
  	alert("你单机了div2");
  }
  document.getElementById("d3").onclick=function(){
  	e = e||window.event;
  	e.stopPropagation();
  	alert("你单机了div3");
  }
  ```

  ```javascript
  document.getElementById("d2").onclick=function(){
  	alert("你单机了div2");
  }
  document.getElementById("d3").onclick=function(e){
  	e=e||window.event;
  	if(e.stopPropagation){
  		e.stopProgation();
	}else{
  		e.cancelBubble=true;
  	}
  	alert("你单机了div3");
  }
  ```
  
  ```javascript
  document.getElementById("d1").addEventListener("click",testa,true);
  function testa(){
  	alert("你单机了div1");
  }
  document.getElementById("d2").addEventListener("click",testb,true);
  function testb(){
  	alert("你单机了div2");
  }
  document.getElementById("d3").addEventListener("click",testc,true);
  function testc(){
  	alert("你单机了div3");
  }
  ```
  
  

## 11.5 事件流

### **冒泡型事件流--由内向外--默认的情况（只要3嵌套在2和1的里面，会由内向外依次触发）**

### **捕获型事件流--由外向内--很少用**

### **事件冒泡**:多个嵌套的元素同时绑定同一个时间，那么在触发的时候，触发当前最内层的元素，这些事件会有由内向外依次进行触发，这种事件成为冒泡型事件，并且默认的事件流是冒泡型事件。

* 如果想用捕获需要用addEventListener()，正常的情况下是冒泡，只能阻止冒泡

* attackEvent("onclick",testa):是不存在冒泡和捕获的，默认是谁就是谁

* 只要加了return false了后面无论有什么都不执行

### **事件委派/事件委托：委派给父元素，这样的话看起来就像是每一个子元素都有这个事件，他解决了加载时间的问题**

### **事件通用函数**

封装里不一样的内容：对象，事件，处理函数

addEventListener(事件，函数，false默认【冒泡】/true捕获) 

```javascript
/*事件通用函数*/
/*对象.addEventListener(事件名，处理函数，false)*/
/*对象.attachEvent("on"+事件名，处理函数*/
function publicEvent(_element,_event,_fun){
	if(_element.addEventListener){
		_element.addEventListener(_event,_fun,false);
	}else{
		_element.attackEvent("on"+_event,_fun);
	}
}
var u=document.getElementsByTagName("ul")[0];
function testa(){
    alert("你单机了这个ul");
}
publicEvent(u,"click",testa);
```

### scrollTop,scrollLeft

scrollTop 向上滚动的距离 用法：对象.scrollTop

scrollLeft 向左滚动的距离 用法: 对象.scrollLeft

```javascript
console.log(document.documentElement.scrollLeft);
/*scrollTop:向上滚进去的距离 用法:对象.scrollTop*/
/*scrollLeft:向左滚进去的距离 用法:对象.scrollLeft*/
document.body.scrollTop;
document.documentElement.scrollTop
```

onsubmit="return false"



# 第十二章 重排、重绘、重构

## 1. 页面重构

1. 页面任何的变化都可以称为页面重构

   我们目前是模块化开发

   整合两种方式：

   本地整合

   服务器整合

2. 组件化开发

   react、vue

3. 测试工具的使用

   各个浏览器、手机、电脑、屏幕

4. 预留空间

   注释

5. 版本控制工具

   GIT

6. 新与稳定技术的选择

   老版本更稳定

7. 编码标准统一

   格式统一、代码统一、

8. 自动化工具

   gulp打包

9. 资源存储

   cookies会影响加载速度

10. 响应式布局

    响应各个不同的分辨率/屏幕

## 2.document.write和innerHTML的区别:

document.write重排整个页面

innerHTML重绘页面的一部分

## 3.浏览器运行机制

构建DOM树

构建渲染树

布局渲染树

绘制渲染树

## 4.浏览器重绘--外观

当盒子的位置、大小以及其他属性。外观改变

## 5.浏览器重排--页面重新加载

隐藏、尺寸、布局改变

某些元素本身已经加载好了 但是由于样式的设置从而重新加载使它显示出来的过程叫做回流

例如：鼠标划入：本来已经把划入出来的内容加载出来了 但是需要鼠标触发才可以加载

* 重绘和重排的关系：

  重排必定会引起重绘，但重绘不一定会引发重排

### 5.1触发重排的条件

1. 页面渲染初始化(无法避免)
2. 添加或删除可见的DOM元素
3. 元素位置的改变，或者使用动画
4. 元素尺寸的改变——大小，外边距，边框
5. 浏览器窗口尺寸的变化

## 6.优化

1.减少对DOM的操作  找对象不算操作对象  给他加上东西才算

2.让引起多次回流的元素，脱离文档流

3.对样式进行修改的时候一次修改，尽量使用className

创建h1



3.

4.图片的设置 盒子模型

# 第十三章 CSS与JS

导航类、固定浮动、滚动图(焦点图)、表单类、淘宝的特效、鼠标划入显示

## 导航类

原理：通过滚动条判断body向上滚动的距离，然后让nav固定或者是跟着动

```html
<div id="header"></div>
<div id="nav"></div>
```

```javascript
window.onscroll=function(){
	if(document.body.scrollTop>200||document.documentElement.scrollTop>=200){
		document.getElementById("nav").style.cssText="position:fixed;top:0px";
	}else{
		document.getElementById("nav").style.cssText="position:fixed;top:200px";
	}
}
```

```css
#header{
	height:200px
	background-color:#f00;
}
#nav{
	width:100%;
	height:50px;
	background-color:#0f0;
	position:absolute;
	top:200px;
}
```

作业：返回顶部

## 鼠标划入显示

找同款

```html
<div>
    <img src="../img/1.jpg">
    <p>
        <span>找相似</span>
        <span>找同款</span>
    </p>
    <span>原价999</span>
    <p>现价9.99</p>
</div>
```

```javascript
var di=document.document.getElementsById("div");
for(var i=0;i<di.length;i++){
    di[i].onmouseover=function(){
		this.children[1].style.display="block";
	}
	di[i].onmouseout=function(){
		this.children[1].style.display="none";
	}
}
```

作业：划入表格变色、找相似、

## 滚动图

无缝滚动效果

原理：需要两个框，外面的框控制元素隐藏的，里面框放图片，

设置属性给里面框，滚动滚外面框

```html
<div id="ou">
	<div id="in"><img src="../img/1.jpg"><img src="../img/2.jpg"><img src="../img/3.jpg"><img src="../img/4.jpg"></div><!--需要注意内框元素与元素之间没有空格和换行-->
</div>
```

```javascript
setInterval(function(){
	if(document.getElementById("ou").scrollLeft>=110){/*比实际的像素小10像素否则会往后退*/
        document.getElementById("in").appendChild(document.getElementById("in").firstChild);
        /*当第一张图片被移进去的时候，在最后面追加第一张图片，使它轮播*/
        document.getElementById("ou").scrollLeft=0;
        /*因为始终移动的是110像素，所以重新让他开始给他赋值为0*/
    }else{
        document.getElementById("ou").scrollLeft+=10;/*每次给scrollLeft加像素*/
    }
},500)
/*设置定时器，让图片自动滚动*/
/*实际上移动的每次都是第一张图片，然后再把它追加到后面，以此实现轮播效果*/
```

```css
#ou{
	width:120px;
    height:100px;
    border:#000 solid 1px;
    overflow:hidden;/*外框：设置规定的宽高，如果超出会隐藏，但依旧有隐藏的那些元素*/
}
#in{
    width:400px;/*内框：放图片的框，让图片在一排显示*/
}
img{
    width:120px;
    height:100px;
}
```

## 点击按钮的轮播图

* 原理:点击左按钮，让上一张显示，也就意味着每一次Left的值是+1000

  如果当前在第一张，那么继续点击左按钮，显示的应该是第四张，所以需要判断left不能>0，加=的原因就是就是获取的当前这一刻的值，所以需要=0

  点击右按钮，让下一张显示，那么Left的值就是-1000的，

  如果当前是最后一张的话，那么单击需要重新显示第一张，判断不能<-3000，因为在当前这一刻获取的值是-3000，所以要加=
  
  不能像无缝滚动一样截取，因为他的下标会乱

```javascript
var ina=document.getElementById("in");
document.getElementById("toLeft").onclick=function(){/*当点击左按钮的时候，是让他的上一张显示，如果是第一张那么他的上一张就是最后一张，所以需要一个判断当left的值大于等于0的时候，点击按钮left的值是-3000也就是最后一张图片的位置*/
	if(parseInt(ina.style.left)>=0){/*因为用的是left后面有px所以用parseInt把px去掉*/
		ina.style.left="-3000px";
	}else{
		ina.style.left=parseInt(ina.style.left)+1000+"px";/*在按左按钮的时候Left的值是+1000的，这1000加的是一张图片的宽度，让这张图片往右走所以是+1000*/
	}
}
document.getElementById("toRight").onclick=function(){/*当点击右按钮的时候，是让他的下一张显示，是最后一张的话那么他的下一张就是第一张，所以需要一个判断当前Left值<=-3000的时候，点击按钮right的值是0也就是第一张图片的位置*/
	if(parseInt(ina.style.left)<=-3000){
		ina.style.left="0px";
	}else{
		ina.style.left=parseInt(ina.style.left)-1000+"px";/*让这张图片往左走所以是-1000*/
	}
}
```

```html
<div id="ou">
    <span id="toLeft"></span>
    <div id="in" style="left:0px;"><img src="/img/1.png"><img src="/img/2.png"><img src="/img/3.png"><img src="/img/4.png"></div><!--这里的left是因为js中使用的样式设置是style但是由于设置的都是行内元素所以前提必须得有这个行内属性所以这里给left赋值为0-->
    <span id="toRight"></span>
</div>
```

```css
#ou{
	width:1000px;
    height:300px;
    border:#f00 solid 1px;
    overflow:hidden;
    position:relative;
}
#in{
    width:4000px;
    position:absolute;
}
img{
    width:1000px;
    height:300px;
}
span{
    width:30px;
    height:100px;
    display:block;
    position:absolute;
    top:50%;
    margin-top:-50px;
    z-index:100;
}
#toLeft{
    background:url("../img/banner_ctrl.png");
    left:20px;
}
#toRight{
    background:url("../img/banner_ctrl.png") -30px 0px;
    right:20px;
}
```

## 点击追加到购物车中

```javascript
var p=document.getElementById("shop").children;
var car=document.getElementById("car");
for(var i=0;i<p.length;i++){
    p[i].onclick=function(){
        if(car.hasChildNodes()){//判断是否car中是否有
            //有商品判断点击与购物车中的商品是否一致
            console.log("有商品");
            var y=-1;//借助一个变量给他赋值为-1
            var carChild=car.children;//把car里面的的子元素赋给变量carChild
            console.log(carChild);
            for(var j=0;j<carChild.length;j++){//遍历car里面的子元素
                var c=this.firstElementChild.innerHTML;//当前点击shop中的P下的第一个子元素里的内容
                var ca=carChild[j].firstElementChild.innerHTML;//当前已有的car下的第一个子元素中的内容
                console.log("点击的商品中的内容："+c);
                console.log("购物车中商品的内容："+ca);
                if(c==ca){//如果点击的商品==购物车中的商品就把当前的这个元素的下标赋给y让他继续进行判断
                    y=j;
                }
            }
            console.log(y);
            if(y==-1){//如果没有这个商品
                console.log("没有这个商品，需要添加");
                var pNew=this.cloneNode(true);//把当前选中的这个p复制一份
                var s=document.createElement("span");//创建一个span标签
                s.innerHTML=1;//给标签赋值为1
                pNew.appendChild(s);//在这个P的后面添加s
                car.appendChild(pNew);//最后把复制的这一份追加到car中
            }else{
                console.log("有这个商品，让span+1");
                //y不是-1的的情况下，找到下标为y的最后一个子元素的内容让他等于转换为数值型的下标为y的最后一个子元素的内容+1   也就是给span加1
                carChild[y].lastElementChild.innerHTML=parseInt(carChild[y].lastElementChild.innerHTML)+1;
                // console.log(carChild[y].lastElementChild);
            }
        }else{//第一次点击的时候 直接加商品名数量为1
            var pNew=this.cloneNode(true);//把复制的直接放到car中
            var s=document.createElement("span");
            s.innerHTML=1;
            pNew.appendChild(s);
            car.appendChild(pNew);//把复制内容连同span一起追加到car中
            console.log("第一次添加");
        } 
    }
}
```

```html
<div id="shop">
    <p><b>榴莲</b></p>
    <p><b>芒果</b></p>
    <p><b>山竹</b></p>
    <p><b>荔枝</b></p>
</div>
<h2>购物车</h2>
<div id="car"></div>
```

```css
div{
	border:#f00 solid 1px;
     width:300px;
}
```































