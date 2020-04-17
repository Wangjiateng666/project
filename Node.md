## Node简介

* 把node作为服务器进行使用

* 实现一个完整网站需要：前端页面，数据库，后台——>服务器上运行

* 例如：支持php这个后台语言的服务器是apache，单独运行时无法运行。

* node与apache一样作为的是web的服务器，只要是服务器就有后台语言，所以在node中js为后台语言

* 在浏览器中我们也可以直接操作js，是在控制台中直接写的js，node不光作为的是服务器，还使用js作为后台语言，同时还封装了谷歌的v8 javascript引擎(可以看成浏览器中的控制台)

* 不是所有带js的都是js框架，例如node.js是由c语言来开发，用js作为后台语言来使用的。

## Node作用

* 简单的高性能服务器，高并发
* 高并发：允许一个服务器连接多个通道，每一个通道都允许多人访问。
* 很多人同时访问服务器，每个人都会有一个访问服务器的接口，每个客户在访问服务器的时候会占一定的内存空间，如果一个8g服务器最多允许4000人同时访问，如果想要增加访问人数，那就需要增加服务器内存空间，同时也会增加硬件成本。
* 不增加硬件成本，只增加访问人数，这个时候就可以使用Node来实现了，因为node对高并发处理是很高的，可以把原来的4000人作为4000个通道，或者是增加通道，每一个通道中可以允许多人进行同时访问

## Node的特点

* 运行js
* 依赖于chrome v8引擎进行代码解析
* 事件驱动
* 单进程，单线程
* 非阻塞I/O
* 轻量、可伸缩，适用于实时数据交互应用

## Node的运行机制

事件环机制、非阻塞I/O机制

## 非阻塞I/O机制

node是使用js来开发的，同时也是单线程运行的，当在发送数据请求和接收数据的都是需要时间进行等待的，传统的单线程处理机制是需要等到数据库有返回数据之后，然后再执行之后的代码，这种的运行机制是阻塞的I/O机制，因为阻塞了代码的执行

而node采取的是非阻塞的I/O机制，不会阻塞之后代码的执行，在操作的时候，执行过程是在请求数据库之后，就可以执行后边的代码了，而数据库中的处理结果会返回到方法（函数）中来执行的，这样的话就提高了代码的运行效率。

## 事件环机制

在node中，不具备用户单击或输入文件而触发的事件，但是具有连接客户端服务器，接收客户端提交的数据，停止客户端提交数据等事件，在Node中，在同一时刻只能触发一个事件回调函数，但是在执行这个事件回调函数的途中，可以处理其他的事件，然后返回去继续执行原来事件的处理函数，这种处理机制就是事件环机制。

使用node服务器搭建react或vue的生产环境

## Node的优缺点

优点：

1. 高并发
2. 适合I/O密集型应用

缺点：

1. debug不方便，错误没有stack trace
2. 开源组件库参差不齐，更新快，向下不兼容
3. 可靠性低，一旦代码某个环节崩溃，整个系统都崩溃

## Node的用途

* 当应用程序需要处理大量并发的输入/输出，而在向客户端发出响应之前应用程序内部并不需要进行非常复杂的处理的时候，可以使用node.js来进行应用程序的开发。总的来说NodeJs适合运用在高并发、I/O密集、少量业务逻辑的场景。。
* 例如：聊天服务器，综合服务类网站，电子商务网站的服务器等等。

## Node的构成

1. 模块：需要引入相应的模块才能进行设置——包

例如：想要创建一个http的请求，那么首先需要把http的模块引入进来

```
Node\node_modules\npm\node_modules
这里面放的就是模块，或者是包
```

2. 创建服务器：http（使用最多的）

3. 接收、响应请求：客户端负责发送请求，服务器接收请求和响应请求

## Node中的模块

引入模块使用：require（url）方法进行引入

```js
var http=require("http");
```

## Node环境

有两个环境

1. 常用于运行**.js文件
2. REPL：相当于控制台，可以在这个环境中写js的内容【尖括号】

在js中有变量、函数等内容，同样在REPL运行环境中这些也可以写

在REPL环境中，回车会直接对当前表达式进行运行

* 变量：js中使用var来创建的，在这个环境中直接写（不加var），加上的话表达式的结果为undfined。

* 使用`_`下划线可以访问最近一次使用的表达式

* 可以直接运行函数，将一个表达式或函数可分为多行进行书写，当前表达式未书写完成时，会在表达式的每一行前添加三个小圆点

  ```js
  function test(){
  ...console.log(b);
  ...}
  /自动生成...
  ```

  ```js
  //例题
  var http=require("http");
  http.createServer(function(req,res){
  ... res.writeHead(200,{'Content-type':'text/html'});
  ... res.write('<head><meta charset="utf-8"></head>');
  ... res.end('你好');
  ... }).listen(1377,'127.0.0.1');
  ```

* 运行js文件：

  先找到文件所在的位置，然后使用node 文件名.js，运行即可

  ```
  C:\Users\王加藤>d:
  D:\>cd test
  D:\test>node test.js
  你好
  D:\test>
  ```

* 基础命令

  ```
  .break	重新书写表达式或函数
  .clear	用于清楚repl运行环境的上下文对象中保存的所有变量与函数
  .exit	退出repl运行环境。使用ctrl+d可以代替.exit命令
  .help	该命令将命令行窗口显示所有的基础命令
  .sava filename	该命令将把你在repl运行环境中输入的所有表达式保存到一个文档中
  .load filename	将某个文件中保存的所有表达式依次加载到repl运行环境中
  ```


## Node中的全局作用域及全局函数

* 函数内的变量--->局部变量
* 函数外的变量--->全局变量

js是后台语言，所以也会有全局之分

在node中，一个模块中的变量或函数其实就相当于局部变量或函数，想要在其他地方使用这个变量或者函数的话需要使用exports导出，导入使用的是require方法进行加载

```js
//test.js

var a=10;
//module.exports是对函数或者变量进行导出的，目的是为了让函数或者变量在模块外也能进行使用
module.exports=a;
```

```js
//index.js

//require是加载某一个导出的模块，现在test就是导出的模块，把test模块中的内容放到index这个模块中进行使用
var test=require("./test.js");
console.log(test);
```

在test.js中有变量a，变量a是存在于test模块中的，在index这个模块中获取test模块中a的值

1.把a从模块中导出，使用module.exports进行变量的导出

2.再index模块中使用require进行test模块的加载，然后就可以获取到test中导出的a

**导出函数**

```js
//test.js

var a="lily";
//module.exports是对函数或者变量进行导出的，目的是为了让函数或者变量在模块外也能进行使用
function doSomething(){
    console.log("你好");
}
module.exports={name:a,talk:doSomething};
```

```js
//index.js

//require是加载某一个导出的模块，现在test就是导出的模块，把test模块中的内容放到testa这个模块中进行使用
var test=require("./test.js");
// console.log(test.name);
test.talk();
```

目前使用的js---ECM script的标准--》ES5

* 全局函数：setTimeout(Interval),clearTimeout(Interval)

  取消函数的调用，对象名.unref()

  回复函数的调用，对象名.ref();

  对u定时器或者延迟器使用unref这个方法的话是取消对定时器和延迟器的执行，但是并没有清除

### 检测一个模块是否为主模块

在node.js中定义了一个require.main变量，用于检测一个模块是否为应用程序中的主模块，使用方式（卸载被检测模块文件的内部）

直接通过node运行的模块文件，我们成为是主模块，在react或者vue中我们也会加载一个react文件或者是vue文件，一般我们把这个文件成为是入口文件

```js
if(module==require.main){
	console.log("主模块");
}
```

```js
//test.js
var a=10;
module.exports=doSomething;
function doSomething(){
    console.log(a);
    if(module==require.main){
        console.log("test是主模块");
    }
}
```

```js
//index.js
var test=require("./test.js");
test();
if(module==require.main){
    console.log("index是主模块");
}
```

**require.resolve：**用来查看完整的文件路径【REPL】

`./`代表的是当前路径

```js
D:\>node
Welcome to Node.js v12.14.0.
Type ".help" for more information.
> require.resolve("./test/test.js");
'D:\\test\\test.js'
>    
```

**require.cache：**用来查看缓存【REPL】

```js
console.log(require.cache);
```

**`__filename与__dirname`变量（两个下划线）**【node】

`__filename`变量获取当前模块文件的带有完整绝对路径的文件名

`__dirname`变量获取当前模块文件所在目录的完整绝对路径

## Nodejs模块

Node这个应用程序就是由一个个的模块来构成的，每一个模块就是一个js文件

node中的第三方类库就相当于jQuery

使用第三方类库的原因可以提高开发效率让代码变得简单易读。

http:使用的是require方法进行加载的

* 创建Http模块：

  先引入http模块：

  require("http")-->因为找模块是在node_modules中查找的

  创建http服务器：

  createServer(function(request,response){回调函数代码})

  request：客户端请求

  response：服务器端响应

* 拆分写：on进行绑定

  listen方法进行ip和端口的监听

  close方法关闭服务器

```js
//引入Http模块var 
http=require("http");
//创建http服务器，request代表客户端请求，response代表服务器器端响应
var server=http.createServer(function(request,response){
    
})

//拆分
var server=http.createServer();
server.on("request",function(req,res){
    
})
```

```js
var http=require("http");
http.createServer(function(req,res){
    res.writeHead(200,{"content-type":"text/html"});
    res.write("<head><meta charset='utf-8'></head>");
    res.end("你好");
}).listen(1377,"127.0.0.1")
```

```js
//拆分后
var http=require("http");
var server=http.createServer();
server.on("request",function(req,res){
    res.writeHead(200,{"content-type":"text/html"});
    res.write("<head><meta charset='utf-8'></head>");
    res.end("你好");
})
server.listen(1377,"127.0.0.1");
server.on("listenling",function(){
    console.log("服务器已监听");
})
//server.listen(1377,"127.0.0.1",function(){
//	console.log("服务器已监听")
//})
server.on("connection",function(){
    console.log("服务器建立连接");
})
server.on("error",function(e){
    if(e.code=="EADDRINUSE"){
        console.log("端口号被占用");
    }
})
server.close();
server.on("close",function(){
    console.log("服务器已关闭连接");
})
```

* request：代表请求事件
* listening：代表监听事件，执行listen方法的时候进行监听
* connection：代表建立连接的事件，当建立连接的时候会执行

### 发送响应头部信息

```
writeHead(http状态例如:200,状态码的描述信息,对象【用于指定服务器端创建的相应的头对象】)
res.writeHead(200,{"Content-Type":"text/html"})

然后使用write()方法向客户端响应内容
end：设置显示内容的
```

## npm包

node是由模块构成的，我们可以把每个模块看成一个个的包，使用的时候如果想让当前这个node有指定功能的话就需要安装这些包----安装包使用的是npm包管理工具

安装，更新，删除，都使用npm来操作的

包

* **学习npm包管理工具的原因：**

  react,vue等框架都需要搭建生产环境，使用的是npm来搭建的

##### 文件目录

```
一个详细的包主要包含的内容
package.json
bin->存放二进制文件
lib->存放js文件
doc->存放对包或者包的使用方法的说明文档
test->对包进行单元测试的文件
```

package.json文件

```
name	包名
preferglobal	全局安装，字段值为true和false
description		包说明
version			版本号
author			作者名
maintainers		包维护者信息数组
bugs,bug的提交地址	
licenses	许可证数组
repository	仓库托管地址数组
keywords	关键字数组
dependencies	本包所依赖的包
```

安装命令行

```
以下属于局部安装
npm install 包名
npm install jquery
```

```
以下属于全局安装（好处是都可以使用）
npm install -g 包名
```

一般情况下我们使用局部要多于全局：在哪个项目中使用就在哪个项目中安装即可，最好不要使用全局安装

```
查看全局包的安装路径
npm root -g
C:\Users\王加藤\AppData\Roaming\npm\node_modules
```

```css
/*修改全局包的安装路径*/
npmconfig set prefix "d:\node"
/*查看命令行题是窗口当前目录下所安装的所有包*/
npm list
/*查看全局包的安装路径下的所有包*/
npm list -g
/*卸载提示窗口当前目录下安装的某个包*/
npm uninstall 包名（卸载当前目录下的）
npm uninstall 包名 -g(全局卸载)
/*更新*/
npm update 包名
npm update 包名 -g
```



事件循环机制：

js是单线程的，如果想要增加线程的话用的异步来实现的

主线程在运行的时候，会产生堆和栈，栈中的代码主要是调用外部的api的，也就是说异步是放在栈中的，我们可以把这个异步操作完成之后会返回到消息队列中

运行过程

1.所有的同步任务都是在主线程上执行的，形成一个执行栈

2.在主线程之外，还存在一个消息队列，消息队列存的是执行完成的异步操作

3.一旦执行栈中的同步任务执行完成，系统会按次序执行读取消息队列中的异步任务，在这个过程中被读取的异步任务结束就会进行执行栈，开始执行





循环中程序执行顺序：

程序最开始按顺序执行，遇到同步立即执行，遇到异步，调用异步请求，把执行完成的异步操作放到消息队列中。程序按照顺序执行完成，查询消息队列中是否有等待的消息，如果有的话，那么按照顺序从消息队列中把异步返回的内容放到执行栈中来执行，执行完第一个异步，然后再从消息队列中获取第二个异步的信息，再放到执行栈中进行执行，这个过程是不断重复的

由于主线程不断地重复获取消息、执行消息、再获取消息、执行消息，所以把这个机制成为是事件循环











