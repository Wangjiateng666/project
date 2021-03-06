# 前端工程化

前端工程化是一种思想

把前端项目当成一项系统工程进行分析、组织和构建从而达到**项目结构清晰、分工明确、团队配合默契、开发效率提高的目的。**

1. 开发需求
2. 共享需求
3. 性能需求
4. 部署需求

从开发角度，要解决的问题包括：

1. 提高开发生产效率
2. 降低维护难度

解决方案：

1. 制定开发规范，提高团队协作能力
2. 分治。软件工程中有个很重要的概念叫做模块化开发其中心思想就是分治

从部署角度，要解决的问题主要是资源管理包括：

1. 代码审查
2. 压缩打包
3. 增量更新
4. 单元测试：写项目的过程中在各个浏览器各手机进行测试

要解决上述问题，需要引入构建/编译阶段

## 开发规范

目的：统一团队成员的编码规范，便于团队协作和代码的维护。

## 组件(component)/模块化(module)

组件化：把一个模块划分成一个一个小的内容，例如：展示页面：轮播图、二级导航、信息展示，重心在产品功能上，称为黑盒

模块化：把功能划分为一个模块，重心在设计和开发阶段，称为白盒

## 构建和编译

为了解决部属问题引入构建（build）和编译（compile）

编译面对的是单文件的编译，构建是建立在编译的基础上，对全部文件进行编译。

## 资源管理

构建的核心是资源管理

前端的资源可以分为静态资源和模板。模板对静态资源是引用关系，两者相辅相成，构建过程中需要对两种资源使用不同的构建策略。

## 静态资源

包括js,css,图片等文件

1. 依赖打包：分析文件依赖关系，将同步以来的文件打包在一起，减少http请求数量-->webpack
2. 资源嵌入：比如小于10kb的图片编译为base64格式嵌入文档，减少一次http请求
3. 文件压缩：减少文件体积
4. hash指纹：通过给文件名加入hash指纹，以应对浏览器缓存引起的静态资源更新问题
5. 代码审查：避免上线文件的低级错误

## 模块构建

模板与静态资源是容器与模块的关系。模板直接引用静态资源，经过构建后，静态资源的改动有以下几点：

1. url改变。开发环境与线上环境的url肯定是不同的，不同类型的资源甚至根据项目的CDN策略放在不同的服务器上
2. 文件名改变。静态资源经过构建之后，文件名被加上hash指纹，内容的改动导致hash指纹的改变。

对于模板的构建宗旨是在静态资源url和文件名改变之后，同步更新模板中资源的引用地址。

# webpack

作为前端主流的打包工具（前端资源模块化管理和打包工具）

好处：更好的加载和更新前端的内容

把松散的资源全部打包在一起

单页面应用：在一个项目中只有一个html页面，所有的内容都是在这个html页面中进行呈现的，加载不同的内容分为不同的视图，每一个视图就像之前看到的每一个页面一样，内容呈现是不一样的

* 原理：项目中会有css文件，js文件、图片文件、less、sass等这些文件
* 在使用webpack打包的时候会把除了图片文件之外的所有文件打包成js文件

不用再像之前一样引入css、js，只需要引入打包之后的js文件即可

## webpack的特点

1. 代码拆分

   webpack有两种组值模块依赖的方式，同步和异步。异步依赖作为分割点，形成一个新的块。在优化了依赖树后，每一个异步区块都作为一个文件被打包。

2. Loader（转换器）

   在webpack中只能操作js模块，如果需要操作css的话就需要安装css的转换器到webpack中，这样就可以把css处理成js的模块了

3. 智能解析

   webpack有一个智能解析器，几乎可以处理任何第三方库，无论他们的模块形式是CommonJS、AMD还是普通的JS文件。甚至在加载依赖的时候，允许使用动态表达式require("./templates/"+name+".jade")

4. 插件系统

   webpack还有一个功能丰富的插件系统，大多数内容功能都是基于这个插件系统运行的，还可以开发和使用开源的webpack插件，来满足各式各样的要求

5. 快速运行

   webpack使用异步I/O和多级缓存提高运行效率，这使得webpack能够以令人难以置信的速度快速增量编译

## 安装webpack

```
使用npm安装webpack
npm install webpack-cli -g
npm install webpack -g
```

此时webpack被安装到了全局环境下，可以通过命令行`webpack -h`试试

```
查看版本号
webpack -v
```

使用webpack打包，通常我们会将webpack安装到**项目**中，这样就可以使用项目本地版本的webpack

注意：文件夹的名字不要使用webpack否则会有冲突，涉及到名字都不要使用webpack

```
npm install webpack (--save-dev)
括号中可加可不加
```

* 打包和开启命令

* 需要安装这个命令：

  全局安装（只需要安装一次即可）

  `npm install webpack-dev-server -g`

  局部安装（哪个项目需要在哪个里面安）

  `npm install webpack-dev-server --save-dev`

```
npm install webpack-dev-server --save-dev
```

还需要安装脚手架

```
npm install webpack-cli -save-dev
```

### 配置初始化文件

package.json：用于记录安装的插件，Loader，以及版本号

需要自动初始化完成：npm init

我们需要入口文件（在里面引入css,js等文件），出口文件（打包之后的文件，在html中实际引入的是这个出口文件，他里面有css，js文件）

对于当前这个项目来说，如何识别哪个文件是出口，哪个是入口文件，需要我们手动写一个webpack.config.js文件

在webpack.config.js文件中配置入口文件和出口文件

```js
module.exports={//对这个文件进行导出
    entry:"./main.js",//设置入口文件，需要注意同级下使用./
    output:{
        path:__dirname,//输出文件的保存路径，不包含文件名的完整路径
        filename:"index.js"//出口文件，需要放到index.html中,自动生成的
    }
}
```

## webpack完整打包步骤

* 全局安装：

  `npm install webpack-cli -g`脚手架

  `npm install webpack -g`

  `npm install webpack-dev-server -g`

* 项目安装：

  `npm install webpack-cli (--save-dev)`

  `npm install webpack (--save-dev)`

  `npm install webpack-dev-server (--save-dev)`

  `npm init` 初始化

  `webpack-dev-server`	运行

在浏览器中输入他给的端口号一般是：`localhost:8080`即可显示页面

* 出口文件是自动生成的，所以在上传到服务器的话，直接上传3个文件即可，html文件、出口文件index.js文件，图片文件，就不用像之前一样上传css,js等文件了

## 安装css依赖

因为在webpack中只能用js，不存在对css的操作等内容，所以我们需要手动安装css的依赖，目的是为了让webpack可以对css文件进行打包

* css-loader：处理css文件的转换器
* style-loader：是为了把html和css进行结合的转换器

安装loader

```
npm install css-loader style-loader (--save-dev)
后面的内容选填
```

只要是安装过转换器都必须在`webpack.config.js`文件中进行配置

```js
在原有的基础上写
module:{    //安装过的模块都有哪些
        rules:[     //把所有的转换器都放到rules里进行匹配，规则匹配
            {   //每个转换器都是一个对象
                test:/\.css$/,  //匹配的文件后缀名
                use:['style-loader','css-loader']   //用哪个转换器   顺序不能变先是style-loader然后是css-loader
            }
        ]
    }
```

* test：一个匹配loaders所处理的文件的扩展名的正则表达式（必须）
* loader：loader的名称（必须）

新建css文件，在文件中写上对dom的样式，然后需要在入口文件中告诉webpack对index.css文件进行打包（在main.js文件中对Index.css文件进行引入）

引入方法使用的是：require(url);

### url-loader

如果想要在css中加入图片的话，那么打包就会出现问题，因为没有设置图片的loader

```
安装图片转换器
npm install url-loader
```

配置文件

```
use代表的是用了什么转换器，同时也可以对其他的内容进行配置，例如name格式，图片大小，图片路径等

module:{    
   rules:[     
       {  
          test:/\.css$/, 
          use:['style-loader','css-loader']
	  },{
		 test:/\.(png|jpg|jpeg|gif)$/,
		 use:[{
                loader:'url-loader',
                options:{
                   name:"[name]-[hash:5].min.[ext]",//规定图片名称
                   limit:20000, //图片大小是<=20kb的
                   publicPath:"./",//图片的入口路径是当前
                   outputPath:"./"//图片的出口路径
                    }
                }]
            }
   	  ]
}
```

需要注意：limit的值如果太小图片会加载不出来，如果省略就是正常的不限制

* url-loader解决问题：

  如果图片较多的时候，会发送多个Http请求，就会降低页面的性能，使用url-loader会对图片进行编码，相当于是把图片编码成一个字符串，把这个字符串打包到文件（index.js）中，访问的时候直接引入这个文件就能访问图片了，因为在这个文件中存放的是编码之后的图片的字符串。如果图片较大，编码就会消耗性能，所以我们需要使用file-loader进行文件的读取

### file-loader

文件大小小于limit的时候，会按照base64方式进行解析

大于limit设置的大小，会直接加载文件的方式进行加载，还需要单独对file-loader进行配置

* 安装file-loader

```
npm install file-loader
```

* 配置file-loader

```
module{
	rules:[{
		test:/\.(ttf|svg|woff|eot)$/,
		use:[
			{
				loader:"file-loader",
				options:{}
			}
		]
	}]
}
```

* 服务器端字体：

  font-face

```css
@font-face{
    font-family:"1.ttf";
    src:url("fonts/1.tff");
}
body{
    font-family:1;
    color:#f00;
}
```

**注意：每次修改配置文件都需要重启才能生效**







