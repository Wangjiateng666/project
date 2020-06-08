## 1. 什么是react

由Facebook开发的专注于UI的库

使用框架：写起来简单方便。周期短。组件化开发

原生js：稳定性强。周期长。需要搭框架

## 2. 组件化开发

组件化开发特点：每一部分可以划分为一个组件，需要时直接引入即可。

MVC：

* M(model)：模型（业务模型）:用于封装与应用程序的状态，响应状态查询，应用程序的功能，通知试图改变
* V(view)：视图（用户界面）：解释模型，模型更新请求，发送用户输入给控制器，允许控制器选择视图
* C(controller)：控制器：定义应用程序的行为，用户动作映射模型的更新，选择响应的视图

用一种业务逻辑、数据、界面显示分离的方式组织代码的

## 3. React的特点

+ 声明式设计--虚拟DOM
+ 高效--**减少了真实DOM的创建以及真实DOM的对比，所以实现了极大的性能飞跃**
+ 灵活--可以与已知的库/框架很好的配合
+ JSX--是JS语法的扩展，可直接在JS中使用HTML
+ 组件化开发--代码复用
+ 单向数据流--父组件向子组件传值，子组件不能直接去改变值

## 4. React的应用范围

* web端应用
* 原生应用-IOS，Android，Native应用
* Node.Js服务端渲染html

## 5. 工程目录文件简介

* ServiceWorker	PWA（通过网页写手机app）上线到https协议的服务器上  需要联网才能访问，即便第二次访问时断网也可以访问
* App.test.js	自动化的测试文件
* manifest.json       
* index.js    整个项目的入口文件

![Snipaste_2020-05-02_09-46-50](https://i.loli.net/2020/05/03/CK4M78irgxwI53A.png)

## 6. react中的组件

分为函数组件和类组件

* 函数

```jsx
function welcome(props){
	return <h1>Hello,{props.name}</h1>
}
```

应用：

```jsx
const App=(props)=>{
    return (
    	<div>
        	<h1>Welcome {props.title}</h1>
            <p>优秀的{props.title}</p>
        </div>
    )
}
ReactDOM.render(
	<App title="React" />,
    document.querySeletor("#root")
)
```

原理：

```jsx
const app=<h1>Welcome React!!!</h1>
const createApp=(props)=>{
    return (
    	<div>
        	{/*只要是在jsx里要插入js代码，就要加一层花括号，注释也是js*/}
            <h1>Welcome {props.title}</h1>
            <p>优秀的{props.title}</p>
        </div>
    )
}

const app=creatApp({
    title:'React 16.8'
})
```

* class  继承React.Component

```jsx
class welcome extends React.Component{
	render(){
		return(
			<h1>hello,{this.props.name}</h1>
		)
	}
}
```

原理：

```jsx
class App extends React.Component{
    render(){
        console.log(this.props)
        return(
        	<div>
            	<h1>类组件</h1>
                <p>{this.props.desc}</p>
            </div>
        )
    }
}

const app = new App({
    desc:'类组件是继承React.Component的'
}).render()

render(
	app,
    document.querySeletor("#root")
)
```

通常引入的就是一个组件

**必须要引入react，否则无法编译JSX语法**

**render是ReactDOM提供的方法**

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
ReactDOM.render(<App />,document.getElementById('root'));
```

```jsx
<React.StrictMode>严格模式
    <App/> JSX语法
</React.StrictMode>
```

### I.虚拟DOM树的表现方式

虚拟DOM树的表现方式

```js
const appVDom={
	tag:'div',
    attrs:{
        className:'di',
        id:'d1'
    },
    children:[
        {
            tag:'h1',
            attrs:{
                className:'c1',
                id:'first'
            },
            children[
            	'类组件'
            ]
        },{
            tag:'p',
            attrs:null,
            children:[
            	'类组件是继承React.Component'
            ]
        }
    ]
}
```

### II.类的形式

这里是使用类的形式创建的组件，这是JSX的语法，但不是合法的JS代码

```jsx
class App extends Component{
    render(){
        return (
        	<div className="di" id="d1">
            	<h1 className="c1" id="first">类组件</h1>
                <p>类组件是继承React.Component</p>
            </div>
        )
    }
}
```

### III.底层编译

React在真正渲染的时候会把上面的代码编译为下面这个样子来运行，下面的代码就是合法的JS代码

```js
class App extends Component{
    render(){
        return (
            //React.creatElement是一个方法，用于创建一个元素
            //第一个参数理解为标签名，第二个参数理解为标签的属性，剩下的是子元素
            //React.createElement(type,[props],[...children])
            React.createElement(
                'div',
                {
                    className:'di',
                    id:'d1'
                },
                React.createElement(
                    'h1',
                    {
                        className:'cl',
                        id:'first'
                    },
                    '类组件'
                ),
                React.createElement(
                    'p',
                    null,
                    '类组件是继承React.Component'
                )
            )
        )
    }
}
```

### Ⅳ.组件中的样式

1.使用style内联创建

第一层花括号是告诉编译器，我们要在JSX中写JS，第二层花括号是要写一个对象

```jsx
<h1 style={{color:#fff}} >hello</h1>
```

2.使用第三方包`classnames`可动态添加不同的className

安装

```
npm install classnames
```

使用

```jsx
import classNames from 'classNames'
<h1 className=classNames("text-red","a")></h1>

<p className=classNames('a',{'b':true,'c':false})></p>
    //这个标签上只会有a和b没有c
```

3.`styled-components的使用`

安装

```
npm install styled-components -S
```

使用

```js
import styled from 'styled-components'

const Title=styled.h1`    //styled.需要代替的标签
	color:#F00;			//里面的内容类似写css
	font-size:50px;
`
```

4. `react中的sass`

安装

```
npm install sass-loader node-sass -s
```

安装sass依赖以及node-sass

直接在需要使用的文件中引用即可

```
import './index.scss'
```

5. css Modules

**使用css Modules原因：可以提供css局部作用域的能力，让css更可控，避免污染全局样式。**

可以创建后缀为`.module.scss`或`.module.css`文件，用于区分全局样式和局部样式

引入

```js
import style from './style.module.css';
<header className={style.title}></header>
```

style.modules.css

```css
.title{
    color:red;
}
```

这种方式会自动给类名加上哈希值，避免类名的重复

* 其他用法

  * 局部变量和全局变量

    :local  做localldentName规则处理 （类名进行编译 默认可以不写）局部

    ```
    :local(.title){
    	color:red;
    }
    ```

    :global   不会有哈希值，相当于`className="title"，默认类名`  会引用全局类

    ```
    :global(.title){
    	color:green;
    }
    ```

  * compose组合class（可以进行样式复用）

    同文件下：

    ```css
    .bg{
    	background:blue;
    }
    .title{
    	composes:bg;
    	color:whilt;
    }
    ```

    不同文件：

    ```css
    /* color.css */
    .red{
        color:red;
    }
    .blue{
        color:blue;
    }
    
    /* index.css */
    .red{
        color:red;
    }
    .header{
        font-size:32px;
    }
    .title{
        color:green;
        composes:blue from './color.css';
    }
    ```

  * CSS和JS变量共享（:export 关键字可以把 CSS 中的 变量输出到 JS 中）

    ```js
        /* index.scss */
        $primary-color: #f40;
    
        :export {
          primaryColor: $primary-color;
        }
    
        /* app.js */
        import style from 'index.scss';
    
        // 会输出 #F40
        console.log(style.primaryColor);
    ```

    



### V.函数组件与类组件

定义组件有两个要求：

1. 组件名称必须以大写字母开头
2. 组件的返回值只能有一个根元素

#### 函数组件

```js
function Welcome (props) {
  return <h1>Welcome {props.name}</h1>
}
ReactDOM.render(<Welcome name='react' />, document.getElementById('root'));
```

函数组件接收一个单一的 `props` 对象并返回了一个React元素

#### 类组件

```js
class Welcome extends React.Component {
  render() {
    return (
      <h1>Welcome { this.props.name }</h1>
    );
  }
}
ReactDOM.render(<Welcome name='react' />, document.getElementById('root'));
```

1. 无论是使用函数或是类来声明一个组件，它决不能修改它自己的 props。
2. 所有 React 组件都必须是纯函数，并禁止修改其自身 props 。
3. React是单项数据流，父组件改变了属性，那么子组件视图会更新。
4. 属性 props 是外界传递过来的，状态 state 是组件本身的，状态可以在组件中任意修改
5. 组件的属性和状态改变都会更新视图。

#### 区别

函数组件和类组件当然是有区别的，而且函数组件的性能比类组件的性能要高，因为类组件使用的时候要实例化，而函数组件直接执行函数取返回结果即可。为了提高性能，尽量使用函数组件。

函数式组件没有继承React.Component，由于生命周期函数是React.Component类的方法实现的，所以没继承这个类，自然就没法使用生命周期函数。

| 区别               | 函数组件 | 类组件 |
| :----------------- | -------- | ------ |
| 是否有 `this`      | 没有     | 有     |
| 是否有生命周期     | 没有     | 有     |
| 是否有状态 `state` | 没有     | 有     |

## 7. JSX语法

在JSX语法中，如果我们要使用自己创建的组件可以直接通过标签形式来使用定义的组件名即可

例如

```jsx
import App from "./App";
ReactDOM.render(<App />,document.getElementById('root'))
```

注意：组件必须以大写字母开头

return返回的元素必须整体在一个大的元素值中，否则会报错

使用占位符`Fragment`替换掉外层包裹的元素

```jsx
//函数
import React,{Fragment} from 'react';
function TodoList(){
	return(
		<Fragment>
       		<div>
        	</div>
        	<ul>
        	</ul>
		</Fragement>		
	)
}
```

```jsx
//class
import React,{Component,Fragment} from 'react';
class TodoList extends Component{
    render(){
        return(
        	<Fragment>
            	<div></div>
            	<ul></ul>
            </Fragment>
        )
    }
}
```

## 8. React组件化项目的目录结构组织方式

使用VSC中的插件ES7可快速书写组件引入/导出内容

```
rcc+回车   类组件
rfc        函数组件
```

在src目录下建立`components`文件夹，然后在`components`文件夹中建立，以组件名命名的文件夹，随后在里面建立index.js，这样在引入的时候可以少写一层引入，因为会自动找到命名为index.js的文件

![](https://i.loli.net/2020/05/06/zHw78ySNusmci4D.png)

```js
//引入
import TodoHeader from 'xxxx/Todolist' 
//否则需要引入多层
import TodoHeader from 'xxxx/Todolist/Todolist.js'
```

在components目录下还会有一个index.js专门负责导出组件

```js
import TodoHeader from './TodoHeader'
import TodoInput from './TodoInput'

export {
    TodoHeader,
    TodoInput
}
```

另一种写法：仅限于不需要重新处理的情况下

```js
export {default as TodoHeader} from './TodoHeader'
export {default as TodoInput} from './TodoInput'
```

在App.js中

```js
import {
    TodoHeader,
    TodoInput
} from './components'
```

## 9. React中的响应式设计思想和事件绑定

不操作DOM而是操作数据

使用变量的时候需要使用`{}`括起来

```jsx
<input value={this.state.inputValue} />
```

绑定事件react：on后的单词首字母要大写

```jsx
<input value={this.state.inputValue} onChange={this.handleInputChange.bind(this)} / >
```

使用箭头函数：

```js
handleAddClick = () =>{
	console.log(this.state)
}
```

使用普通函数：

```js
handleAddClick () {
	console.log(this.state)
}
```

如果直接这样去写会报错，因为this的指向不对，所以需要在绑定的时候需要使用bind改变this的指向

```js
onClick={this.handleAddClick.bind(this)}
```

同时bind可以传递参数

```js
onClick={this.handleAddClick.bind(this,123)}
```

```js
handleAddClick (id) {
	console.log(this.state,id)   //   123
}
```

但是这种写法并不好，因为render中的内容，只要数据改变就会执行一次，所以要把他写在constructor中，因为constructor只执行一次

```js
constructor(){
    this.handleAddClick = this.handleAddClick.bind(this)
}
```

* e.target：指向触发事件监听的对象
* e.currentTarget：指向添加监听事件的对象

### setState()`是异步的`

直接去修改state是不允许的，尽管可以修改，但是页面不会重新渲染，因此我们使用setState()方法

改变`constructor`中的状态使用`setState()`方法向里面传入对象的形式来改变，**`setState`是异步的（为了提升react底层的性能）**，setState()可以有两个参数：上一次的state和上一次的props

第一个参数有两种情况：

第一种情况是一个对象：

```jsx
this.setState({
    isLiked:!this.state.isLiked
})
```

第二种情况是一个方法：可以输出上一次State的值，可以避免修改state的状态

```js
this.setState((prevState)=>{
    console.log(prevState)
	return {
		isLiked: !prevState.isLiked
	}
})
```

```jsx
handleBtnClick(){
	this.setState((prevState) => ({
		list:[...prevState.list, prevState.inputValue],
		inputValue:''
	}))
}
```

第二个参数：

```jsx
handleBtnClick(){
	this.setState((prevState) => ({
		list:[...prevState.list,prevState.inputValue],
		inputValue:''
	}))
	console.log(this.ul.querySelectorAll('div').length);
}
```

上面的这段代码根据`input`添加的项，依次是0，1....，每次都会比实际的长度少1个，原因是`setState()`本身是异步函数，他不会立即执行，也就是说`console.log`是在`this.setState`运行之前去执行的。所以如果希望`setState()`执行成功之后，页面更新之后，再去获取页面上的DOM，正确的做法是，setState()中提供给我们了一个第二个参数，当setState()完全的执行好了之后，他的第二个参数（一个回调函数）会被执行

```jsx
handleBtnClick(){
	this.setState((prevState) => ({
		list:[...prevState.list,prevState.inputValue],
		inputValue:''
	}),() => {
      	console.log(this.ul.querySelectorAll('div').length);  
    })
}
```

![](https://i.loli.net/2020/05/06/zfOc9EDe7ABtPIQ.png)

setState是异步的

```js
handleLikedClick=()=>{
        this.setState((prevState)=>{
            console.log('setState内部的this.state.isLiked',this.state.isLiked);
            return {
                isLiked:!this.state.isLiked
            }
        })
        console.log('setState外部的this.state.isLiked',this.state.isLiked);
}
```

**`setState`可以把多次对`setState`的修改合并为一次，减少对虚拟DOM修改的次数**

### 深度剖析setState()

1. `setState` 只在合成事件和钩子函数中是“异步”的，在原生事件和 `setTimeout` 中都是同步的。

2. `setState`的“异步”并不是说内部由异步代码实现，其实本身执行的过程和代码都是同步的，只是合成事件和钩子函数的调用顺序在更新之前，导致在合成事件和钩子函数中没法立马拿到更新后的值，形式了所谓的“异步”，当然可以通过第二个参数 setState(partialState, callback) 中的callback拿到更新后的结果。

3. `setState` 的批量更新优化也是建立在“异步”（合成事件、钩子函数）之上的，在原生事件和setTimeout 中不会批量更新，在“异步”中如果对同一个值进行多次 `setState` ， `setState` 的批量更新策略会对其进行覆盖，取最后一次的执行，如果是同时 `setState` 多个不同的值，在更新时会对其进行合并批量更新。



### setState()中踩坑点

在修改state中数组的时候不要使用push，因为push返回的值是一个数组长度，而非值

```js
//容易踩坑的地方，push返回的是一个数组长度，而不是值
//错误写法！！！
this.setState({
   todos:this.state.todos.push({
   id:Math.random(),
   title:todoTitle,
   isCompleted:false
   })
})
```

正确写法是：map或concat

```js
this.setState({
     todos:this.state.todos.concat({
       id:Math.random(),
       title:todoTitle,
       isCompleted:false
     })
})
```

## 10. TODOLIST新增删除

在遍历的时候要给遍历的对象加上一个`key`属性，否则会有一个警告，`不建议直接写index`

```jsx
this.state.list.map((item,index)=>{
	return <li key={index}>{item}</li>
})
```

`immutable`即state不允许我们做任何的改变，需要借助变量

```jsx
handleItemDelete(index){
	const list=[...this.state.list];
	list.splice(index,1);
	this.setState({
		list:list
	})
}
//这里的操作是拷贝了一个副本最后赋值给list，而不是直接去改变
```

## 11. JSX语法细节点

### 注释

```jsx
{/*注释内容*/}

单行注释需要占三行
{
    //注释内容
}
```

### className

在react中给标签添加`class`需要使用的是`className`属性，因为react认为`class`与`class`类同名会混淆。

```jsx
<input className="input" />
```

### dangerouslySetInnerHTML

不希望某些内容被转义

```jsx
<li dangerouslySetInnerHTML={{__html:this.state.item}}></li>
//在__html这个属性中写要不转义的内容
```

例如：输入`<h1>内容</h1>`会被写成`h1`标签的格式

### `label`标签中的`for`属性

`react`会认为`for`是指循环，所以发生同名冲突，于是`react`中`label`标签的`for`是`htmlFor`，如果写成`for`会有一个警告

```jsx
<label htmlFor="insertArea"></label>
```

## 12. 拆分组件与组件之间传值

### props

获取父组件上的属性：`this.props.属性名`

获取标签中的内容：`this.props.children`

传递数字时需要加上花括号`x={1} y={2}`

#### prop-types

强校验——限制传值的类型

可以使用prop-types检验数据类型，以及设置必填项

安装

```
npm install --save prop-types
```

函数式组件的书写：组件名.propType

```js
import PropTypes from 'prop-types';
TodoHeader.propTypes={
    desc:PropTypes.string,   //类型需为string
    x:PropTypes.number.isRequired,  //类型需为number且不为空
    y:PropTypes.number.isRequired
}
```

类组件的书写：

```jsx
class TodoHeader extends Component{
	static propType={
        btnText:PropTypes.string
    }
}
```

#### defaultProps

默认传输——为空时传

函数式组件：

```js
TodoHeader.defaultProps={
    desc:'明日复明日，明日何其多'
}
```

类组件：

```JS
class TodoHeader extends Component{
	static defaultProp={
		btnText:"添加TODO"  //如果不设置btnText就显示defaultProp中设置的内容
	}
}
```

### state

组件自己本身的状态

```js
class App extends Component{
	constructor(){
        super()
        this.state={
            title="待办事项列表",
            desc="今日事，今日毕",
            article="<h1><i>自强不息</i></h1>",
            todos:[{
            	id:1,
            	title:'学习react',
            	isCompleted:true
        	},{
            	id:2,
            	title:'学习redux',
            	isCompleted:false
        	}]
        }
    }
}
```

完全受控组件：所有的状态是没有的，都是通过props获取的外部数据

非受控组件：有自己的状态

半受控组件：一部分是自己的状态，一部分是props获取的

```jsx
//三元运算符
{this.state.todos[0].isCompleted ? "完成" : "未完成"}

//不转义
{
    <div dangerouslySetInnerHTML={{__html:this.state.artcle}}></div>
}

//遍历输出
{
     this.state.todos.map(todo=>{
        return <div key={todo.id}>{todo.title}</div>
     })
}
```

### props和state区别

* props是可变的
* state是根据与用户交互来改变

props

```jsx
//父元素
{
    this.state.list.map((item,index){
         return(
         	<div>
            	<TodoItem content={item} index={index} deleteItem={this.handleItemDelete}.bind(this) />            
            </div>       
         )               
    })
}
```

```jsx
//子元素
<div onClick={this.handleClick}>
	{this.props.content}//属性
</div>
handleClick(){
    this.props.deleteItem(this.props.index); //方法
}
```

### 组件之间的传值

祖先组件：

```js
this.state={
            title:'待办事项列表',
            desc:'今日事，今日毕',
            artcle:'<h4><i>知识改变命运</i><u>running</u></h4>',
            todos:[{
                id:1,
                title:"吃饭",
                assignee:"August",
                isCompleted:true
            },{
                id:2,
                title:"睡觉",
                assignee:"why",
                isCompleted:false
            }]
}
```

父组件：

```js
			{
                    this.props.todos.map(todo=>{
                        return (
                            // <TodoItem 
                            //     key={todo.id} 
                            //     id={todo.id}
                            //     title={todo.title}
                            //     isCompleted={todo.isCompleted}
                            // />
                            <TodoItem         //上面的形式可以简写为下面这种，展开式
                                key={todo.id}
                                {...todo}   
                            />
                        )
                    })
                }
```

子组件：

```js
render() {
        console.log(this.props);  //可以获取完整展开形式
        return (
            <li>
                {this.props.title}  {this.props.isCompleted ? "完成" : "未完成"}
            </li>
        )
}
```



## 13. Todolist代码优化

ES6return的简写

```jsx
//简写前
handleInputChange(e){
    this.setState(()=>{
        return {
            inputValue:e.target.value
        }
    })
}
```

```jsx
//简写后
handleInputChange(e){
    this.setState(() => ({
        inputValue:e.target.value
    }))
}
```

## 14. 单向数据流

父组件可以向子组件传值，但是子组件不能直接的去改变的值

例如：在一个组件中修改了值，在其他的组件中也使用了这个值，所以其他的组件也会跟着变，一旦出现bug，会给调试带来很大的麻烦

### 解决方法

父组件传递给子组件一个方法，在子组件中调用父组件传递的方法，然后去做修改，实际上是父组件的方法对数据进行改变的

### arrayOf()语法

或   **指的是数组中的数据类型是number/string**

```jsx
TodoItem.propTypes = {
	content: PropTypes.arrayOf(PropType.number,PropType.string) //类型是number或者string
}
```

### oneOfType

语法：`oneOfType( [] )` 传的值是一个数组

是括号中任意一种类型即可   或

```jsx
TodoItem.propTypes = {
	test: PropTypes.oneOfType([PropTypes.number,PropTypes.string]);
}
```

## 15. Props,State与render函数

当组件的`state`或者`props`发生改变的时候，render函数就会重新执行

```jsx
//父向子传
<Test content={this.state.inputValue} />
//子接收父
<div>{this.props.content}</div>
```

**当父组件的`render`函数被运行时，他的子组件的`render`也将被重新运行一次**

1. props改变
2. 是父组件的子组件

## 16. 虚拟DOM

虚拟DOM就是一个JS对象，用它来描述真实DOM

例如

```jsx
//真实DOM
<div id="abc"><span>hello world</span></div>
//生成虚拟DOM
['div',{id:'abc'},['span',{},'hello world']]
```

**减少了真实DOM的创建以及真实DOM的对比，所以实现了极大的性能飞跃**

```jsx
1.state数据
2.JSX模板

3.数据 + 模板  生成虚拟DOM （虚拟DOM就是一个JS对象，用它来描述真实DOM）   （损耗了性能）
['div',{id:'abc'},['span',{},'hello world']]

4.用虚拟DOM的结构生成真实的DOM来显示
<div id="abc"><span>hello world</span></div>
    
5.state 发生变化

6.数据 + 模板 生成新的虚拟DOM （极大的提升了性能）
['div',{id:'abc'},['span',{},'bye bye']]

7.比较原始虚拟DOM和新的虚拟DOM的区别，找到区别是span中的内容    （极大的提升了性能）
8.直接操作DOM，改变span中的内容
```

## 17. 深入了解虚拟DOM

回到代码中理解，是先把`JSX模板`转换成`JS对象`然后转换为`真实的DOM`

```jsx
render(){
	return (
		<div>item</div>    
        //JSX模板
	)
}
```

实际上`react`底层会把`JSX模板`通过`creatElement`t转换为`JS对象`，即下面的形式

```jsx
return React.createElement('div',{},'item') //标签 属性 内容
```

优点：

1. 性能提升
2. 它使得跨端应用得以实现。React Native

## 18. 虚拟DOM中的Diff算法

`Diff`全称`diffrence`

### 同级比较

同层比对，对一层DOM比较，如果一致，比较第二层，如果不一致，react就不会继续往下比较，于是把原始页面上的虚拟DOM对应下面所有的节点的DOM全部删除，重新生成一遍下面所有的节点的DOM，然后用重新生成的节点的DOM去替换原始页面上的DOM

同级比较，算法会简单，且速度会很快，尽管可能会造成DOM重新渲染上的浪费，但他大大减少了两个虚拟DOM在比对上的性能消耗

### 不要使用index作为key值

**引入key值实际上是为了提高虚拟DOM比对的性能**

通过Todolist添加了三个列表项，分别为a、b、c，他们的index值：a-0，b-1，c-2，这个时候删除a，他们的index值就会发生变化：b-0，c-1 。以前的b和现在的b无法建立起关系，key值就不稳定，key值也就失去了意义。

解决：

可以使用他的值作为key值，尽量要使用一个稳定的值

例如：a-a，b-b，c-c。删除a，b依旧对应b，c依旧对应c

## 19.ref

react通过ref来获取组件或者DOM元素

获取触发事件的元素对应的`DOM`

使用场景：

* 管理焦点，文本选择或媒体播放
* 触发强制动画
* 集成第三方DOM库

ref 是使用 `React.createRef()` 创建的，并**通过 `ref` 属性附加到 React 元素**。在构造组件时，通常将 ref 分配给实例属性，以便可以在整个组件中引用它们。

```js
import React,{ Component,createRef } from 'react'
```

```jsx
<input ref={(input) => {this.input=input}} />
```

例子：

```js
//清空input之后获取焦点
handleAddClick=()=>{
	this.props.addTodo(this.state.inputValue)
	this.setState({
		inputValue:''
	},()=>{
		this.inputDom.current.focus()
	})
}
```

```js
//想获得谁的真实DOM只需要给他一个ref属性即可，
<input type="text" ref="myInput" />
this.setState({
	msg:this.refs.myInput.value
})
```



## 20. 生命周期

生命周期是针对于组件的，每一个组件都有这些生命周期

定义：生命周期函数指在某一个时刻组件会自动调用执行的函数

render()

组件的生命周期可分为三个状态：

1. Mounting：已插入真实DOM   **`挂载`**
2. Updating：正在被重新渲染   **`渲染`**
3. Unmounting：已移出真实DOM   **`卸载`**

### componentWillMount()  `已过时改用componentDidMount()`

在组件即将被挂载到页面的时刻自动执行

### componentDidMount()

组件被挂载到页面之后，自动被执行

### shouldComponentUpdate()

组件被更新之前，他会自动被执行。**做的是浅比较**

语法：`shouldComponentUpdate(nextProps,nextState)`

```js
shouldComponentUpdate(){//是否需要更新你的组件？
	return true;	//如果是false则不更新
}
```

如果`retrun false`那么后面整个的流程都不会进行

```js
    shouldComponentUpdate(nextProps,nextState){
        return nextProps.isCompleted !== this.props.isCompleted
    }
```

有时候进行的比较可能会不那么准确，所以我们会借用一些第三方库。例如lodashi中的`_.isEqual(value,other)`，属于深度比较，比较耗费性能 

```js
var object={'a':1};
var other={'a':1};
_.isEqual(object,other)  //true

object===other  //false
```

在react中，也有专属于react的，使用`{ PureComponent }`库，可不需要去做比较

```js
import React,{PureComponent} from 'react'
export default class TodoItem extends PureComponent
```

但是PureComponent只做了第一层比较，是浅比较，如果套的层次更深就还需要再做一次shouldComponentUpdate

### componentWillUpdate() `已过时改用componentDidMount()`

组件被更新之前，自动执行，但是他在shouldComponentUpdate之后执行，如果shouldComponentUpdate返回true执行，否则不执行

### componentDidUpdate()

组件更新完成之后，会被执行

### componentWillReceiveProps() `已过时` 

当一个组件要从父组件接收了参数，只要父组件的`render`函数被重新执行了，子组件的这个生命周期函数就会被执行

需要满足三个条件：

1. 一个组件要从父组件接收了参数
2. 如果这个组件第一次存在于父组件中，不会执行
3. 如果这个组件之前已经存在于父组件中，才会执行

替代：

- 如果你需要**执行副作用**（例如，数据提取或动画）以响应 props 中的更改，请改用 [`componentDidUpdate`](https://zh-hans.reactjs.org/docs/react-component.html#componentdidupdate) 生命周期。
- 如果你使用 `componentWillReceiveProps` **仅在 prop 更改时重新计算某些数据**，请[使用 memoization helper 代替](https://zh-hans.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#what-about-memoization)。
- 如果你使用 `componentWillReceiveProps` 是为了**在 prop 更改时“重置”某些 state**，请考虑使组件[完全受控](https://zh-hans.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#recommendation-fully-controlled-component)或[使用 `key` 使组件完全不受控](https://zh-hans.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#recommendation-fully-uncontrolled-component-with-a-key) 代替。

```js
//老版本的坑：Constructor里面通过props来初始化了一个state,在props修改之后，这个state不会再次更新
constructor(props){
    super()
    this.state={
        completedText:props.isCompleted ? '完成' : '未完成'
    }
}
//那么就需要借助于componentWillReceiveProps来做一次修正
UNSAFE_componentWillReceiveProps(nextProps){
    this.setState({
        completedText:nextProps.isCompleted ? '完成' ：'未完成'
    })
}
```

### getDerivedStateFromProps(props, state)

是componentWillReceiveProps的替代

```
组件每次被render的时候，包括在组件构建之后(虚拟dom之后，实际dom挂载之前)，每次获取新的props或state之后；每次接收新的props之后都会返回一个对象作为新的state，返回null则说明不需要更新state；配合componentDidUpdate，可以覆盖componentWillReceiveProps的所有用法
```

```js
    constructor(){
        super()
        this.state={
            CompletedText:''
        }
    }

    static getDerivedStateFromProps(props){
        return {
            CompletedText:props.isCompleted ? '完成' : '未完成'
        }
    }
```

getSnap

### componentWillUnmount()

当这个组件即将被从页面中剔除的时候，会自动执行

## 21. 生命周期的使用场景

### 优化

例如：当父元素内容改变的时候，子元素也会跟着被渲染一次，造成浪费。

原因：当父组件的`render`函数被运行时，他的子组件的`render`也将被重新运行一次

解决：通过`shouldComponentUpdate(nextProps,nextState)`进行优化，判断子元素中的数据是否进行了修改。

```js
shouldComponentUpdate(nextProps,nextState){
	if(nextProps.content !== this.props.content){
		return true;
	}else{
		return false;
	}
}
```

### Ajax--axios

`react`中的`Ajax`会被放在`componentDidMount()`中，之所以不能放在`render`中就是因为`render`这个函数会反复的执行，只要数据发生变化就会执行，从而造成死循环。而`componentDidMount()`在组件被挂载到页面上的时候，会执行一次。之后不会被重新的执行

**axios:基于promise用于浏览器和node.js的http客户端**

1.安装`axios`

```
yarn add axios 
```

2.引入`axios`

```
import axios from 'axios'
```

3.在`componentDidMount()`中使用`axios`

```js
componentDidMount(){
	axios.get('/api/todolist')
		.then( () => {alert('success')}) //成功 
		.catch( ()=> {alert('error')})  //失败
}
```

4.控制台中查看`NetWork`选择All会看到有一个请求是从`localhost:3000/api/todolist`发出的



如果想要全局的扩展React.Component的prototype，比如：想把ajax的方法全局挂载到组建的this上，既可以使用下面的方式

index.js

```js
//引入所有的ajax请求
import * as Services from './services'
//在prototype上挂载一个叫http的东西，然后就可以在组件内部通过this.http.方法名来执行一些操作
React.Component.prototype.http=services
```

Services/index.js

```
import axios from 'axios'
import apis from './apis'

const ajax=axios.create({
    baseURL:apis.baseURL
})

// 全局的拦截器处理
export const getTodos=()=>{
    return ajax.get(apis.todos)
}
```

Services/apis.js

```
export default {
    baseURL:'https://jsonplaceholder.typicode.com',
    //获取todos的接口
    todos:'/todos'
}
```

## fetch

fetch是将jQuery ajax封装再用promise进行封装

```js
        fetch("./mock/data.json")
        .then(response=>{
            console.log("服务器返回来的信息 头 数据",response);
            console.log(response.headers.get('Date')); //日期
            console.log(response.status);	//状态码
            console.log(response.statusText);	//状态
            return response.json(); //数据是json格式的话使用的方法
            //return response.text() 数据是字符串格式
        })
        .then(data=>{
            this.setState({
                myData:data.data
            })
        })
        .catch(e=>{	//错误处理
            alert(e)
        })
```



## 22. Hooks

函数组件是没有生命周期的，Hooks是为了解决这个问题而生的，可以让函数式使用类组件的一些特性。

**useState（初始值，修改状态的方法）**

这个方法的参数就是默认值。结果是一个数组，数组的第一个就是state，第二个就相当于setState

```js
import React,{useState} from 'react'
const Counter=()=>{
	const [count,setCount]=useState(0)
	return (
		<>
        	//这里的setCount就是useState所生成的方法。注意和setState不一样的地方在于参数，这里的参数就是一个新值即可。
			<button onClick={()=>{setCount(count - 1)}}></button>
			//这里是useState创建的值
			<span>{count}</span>
			<button onClick={()=>{setCount(count + 1)}}></button>
		</>
	)
}
```

**useEffect（回调函数）**

useEffect的参数是一个回调，不管是组件挂载还是更新，都会触发这个回调函数，类似于componentDidMount 和componentDidUpdate的结合

```js
import React,{useEffect} from 'react'
const Counter=()=>{
	useEffect(()=>{
		console.log('更新了')
	})
}
//类似与componentDidMount componentDidUpdate
```

## 23. Context

Context 提供了一个无需为每层组件手动添加 props，就能在组件树间进行数据传递的方法。

引入：createContext是react提供的一个跨组件传值的方法

```js
import React,{ createContext,Component } from 'react'
```

React.createContext：创建一个上下文的容器（组件），defaultValue可以设置共享的默认数据。这个方法的结果是一个对象

```js
const {Provider,Consumer}=React.createContext(defaultValue)
```

Provider(提供者/生产者)：看名字就知道他是用来提供或产生共享数据的地方。value：放置共享的数据

```jsx
<Provider value={共享的数据} >
	渲染的内容
</Provider>
```

Consumer(消费者)：专门消费供应商（Provider）产生的数据的。Consumer需要嵌套在生产者下面，才能通过回调的方式拿到共享的数据源。当然也可以单独使用，那就只能消费到上文提到的defaultValue

**注意：Consumer的children必须是一个方法，这个方法有一个参数，这个参数就是Provider的value**

```JSX
<Consumer>
	{value=>根据上下文进行渲染响应内容}
</Consumer>
```

## 24. HOC

HOC高阶组件：Higer-Order Component

```js
var add=(x)=>{  //这一层叫做高阶函数
	return (y)=>{
		return x+y
	}
}
add(1)(2)  //3
```

一个方法里return一个组件就叫做高阶组件

高阶组件在调用的时候为了不覆盖传递的参数，要把参数传递给子组件，向下传递

App.js

```jsx
import React, { Component } from 'react'
import Another from './Another'
 class App extends Component {
    render() {
        return (
            <div>
                App
                <Another name="组件App" />
            </div>
        )
    }
}

export default App
```

Another.js

```jsx
import React, { Component } from 'react'
import WithCopyrigh from './WithCopyrigh'

class Another extends Component {
    render() {
        return (
            <div>
                Another {this.props.name}
            </div>
        )
    }
}

export default WithCopyrigh(Another)

```

WithCopyrigh.js

```jsx
import React, { Component } from 'react'

const WithCopyrigh=(YourComponent)=>{
    return class WithCopyrigh extends Component {
        render() {
            console.log(this.props);
            return (
                <>
                    <YourComponent {...this.props} / >
                    <div>&copy;2019 &emsp; </div>
                </>
            )
        }
    }
}

export default WithCopyrigh
```

## 25. CRA中装饰器的写法支持

让cra支持@装饰器写法

安装

```
npm install react-app-rewired --save-dev
```

1. 使用`react-app-rewired`这个包对`cra`创建的项目进行轻微的配置调整

2. 安装好之后，在packjson.json里把`scripts`里的`rect-scripts`替换成`react-app-rewired`

   ```json
   "scripts": {
       "start": "react-app-rewired start",
       "build": "react-app-rewired build",
       "test": "react-app-rewired test",
       "eject": "react-scripts eject"
   },
   ```

3. 在根目录下创建一个`config-overrides.js`

   ```js
   module.exports=(config)=>{
       //在这里可以对config进行配置
       return config
   }
   ```

4. 当然如果想要配置更方便，可以在安装`customize-cra`，然后把`config-overrides.js`改为

```js
const { override,addDecoratorsLegacy } = require('customize-cra')
module.exports = override (
    addDecoratorsLegacy()
)
```

vue与react的非技术区别：vue的生态更官方化，react更社区化

## 26. redux

通过redux能够更好的管理状态

安装

```
npm install redux
```

以下为原理图

![](https://i.loli.net/2020/05/12/GbaTk6XFrLlEZtS.png)

1. Store——相当于仓库

2. React Compoent——组件

3. Action Creators——行为发出者

4. Reducers——相当于仓库管理员

   **reducer是一个纯函数：不依赖于任何外部输入，不改变任何外部数据、没有副作用。**

   举例说明：

   ```js
   const foo = (x, b) => x + b
   foo(1, 2) // => 3
   ```

   返回的结果只依赖于他的参数，永远都是3，今天是，明天也是

   函数执行的过程中对外部产生了可观察的变化，我们就说函数产生了副作用。

   例如：ajax请求，console.log，刷新页面等等





如果把整个redux比做图书馆借书那么可以这样理解：

![](https://i.loli.net/2020/05/12/hVrLz21EaWmJbyg.png)



1. Store，仓库用于存放状态的，

   createStore是redux中的一个方法，用来创建仓库

   ```js
   import {createStore} from 'redux'
   import reducer from './reducer'
   const store = createStore(reducer)
   export default store
   ```

   可以理解为创建了一个图书馆store，这个图书馆授权给了图书管理员reducer，并对外开放

2. React Components，也就是我们所使用的组件

   ```jsx
   import {Component} from 'react'
   import store from './store'
   export default class App extends Component{
       constructor(props){
           super(props)
           this.state=store.getState()//使用getState()方法把store中的状态给了组件，在组件中就可以自由使用了
       }
   	render(){
   		return (
   			<div>
               	{this.state.inputValue}
                </div>
   		)
   	}
   }
   ```

   可以理解为借书者，使用getState()方法把图书馆`store`中的书(状态)借给了我们，我们可以自由的使用书(状态)
   
3. ActionCreaturs，行为发起者也就是我们使用的Action，用来表示视图发生的变化，有一个固定属性值type，用来区分动作是哪个Action发起的，然后是你要进行操作的属性值，最后要使用store中的dispathch方法直接将获取到的行为发送给Reducer(图书管理软件)

   ```JS
       deleteItem(index){
           const action={
               type:'DELETE_ITEM',
               index
           }
           store.dispatch(action)
       }
   ```

   dispatch是用来发出action的，他会直接把action发给reducers

   可以理解为我们借书者(React Components)找到图书管理员(ActionCreaturs)告诉他我们要借的书，图书管理员记了下来，然后使用了dispatch方法写给了图书管理软件(Reducer)

4. Reducer，缓冲器/减速器

   ```js
   export default (state=defaultState,action)=>{
   	if(action.type==="DELETE_ITEM"){  //检索的图书
   		let newState=JSON.parse(JSON.stringify(state))
            newState.list.splice(action.index,1)
            return newState
   	}
       return state
   }
   ```

   接上一步，图书管理软件直接`检索你所需要的图书`（action.type），如果有就给出反应(视图发生变化)，如果没有就什么也不做，假设找到了你所需要的书，图书管理软件会登记你的信息，最后从图书馆中借书给你
   
5. 在其中还有至关重要的一步是监听，subscribe，一旦state有变化，store就会调用监听函数

   ```js
   export default class App extends Component{
   	constructor(props){
           super(props)
           this.state=store.getState()
           this.stateChange=this.stateChange.bind(this)
           store.subscribe(this.stateChange)
       }
       stateChange(){
           this.setState(store.getState())
       }
   }
   ```

### API

* createStore
* store
* combineReducers
* applyMiddleware
* bindActionCreators
* compose

#### createStore

创建一个redux store用来存放应用中的所有state，一个应用中有且仅有一个store

参数：

1. reducer：接收两个参数，分别是当前的state树和要处理的action，返回新的state树
2. [`preloadedState`] *(any)*: 初始时的 state。 在同构应用中，你可以决定是否把服务端传来的 state 水合（hydrate）后传给它，或者从之前保存的用户会话中恢复一个传给它。如果你使用 [`combineReducers`](https://www.redux.org.cn/docs/api/combineReducers.html) 创建 `reducer`，它必须是一个普通对象，与传入的 keys 保持同样的结构。否则，你可以自由传入任何 `reducer` 可理解的内容。
3. enhancer：`Store enhancer`是一个组合`store creator`的高阶函数，返回一个新的强化过的`store creator`。这与`middleware`相似，它也允许你通过复合函数改变`store`接口

#### Store

`Store`用来维持应用所有的state树的一个对象，改变store内state的唯一途径是对他`dispatch`一个`action`

**Store方法**

* `getState()`
* `dispatch(action)`
* `subscribe(listener)`
* `replaceReducer(nextReducer)`

**getState()**

返回应用当前的`state`树，它与`store`的最后一个`reducer`返回值相同

**dispatch(action)**

分发`action`。触发state改变的唯一途径

会使用当前`getState()`的结果和传入的`action`以同步方式的调用`store`的`reduce`函数。返回值会被作为下一个state

**subscribe(listener)**

添加一个变化监听器。每当`dispatch action`的时候就会执行，`state`树中的一部分可能已经变化。

## 中间件

**中间件指的是action和store的中间**

**中间件的原理：对store的dispatch做一个升级（封装）：之前只能接收一个对象，现在可以接收一个对象也可以接收一个函数**

![](https://i.loli.net/2020/05/14/r34XzhQuxnePgSk.png)

**使用场景：项目日志，崩溃报告**

中间件原理图

![](https://i.loli.net/2020/05/14/CvO51IVotbrLPHy.jpg)

### redux-thunk

Redux store 仅支持同步数据流。使用 `thunk` 等中间件可以帮助在 Redux 应用中实现异步性。可以将 `thunk` 看做 store 的 `dispatch()` 方法的封装器；我们可以使用 `thunk` action creator 派遣函数或 Promise，而不是返回 action 对象。**它返回的是函数{}，而不是对象。**

* **使用redux-thunk之后，action可以是一个函数了，之前是一个对象，可以解决异步问题**
* **dispatch会根据参数的不同，执行不同的事情，如果参数是对象直接传给store，如果参数是函数，就把函数执行结束**

安装

```
npm install --save redux-thunk
```

配置：

由于createStore只能接收两个参数，所以需要借助增强函数

applyMiddleware是redux提供的中间件

使用compose做增强函数：执行完一个函数后再执行一个函数

```js
import { createStore, applyMiddleware, compose } from 'redux'
import reducer from './reducer'
import thunk from 'redux-thunk'
//增强函数，判断是否有这个方法，如果有就调用
const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__?
	window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}):compose
const enhancer = composeEnhancers(applyMiddleware(thunk))
const store = createStore(reducer,enhancer)
export default store
```

### 与redux-saga的区别

* **redux-saga：单独的把异步的逻辑拆分出来，放到另一个文件中进行管理**
* **redux-thunk：把异步放到action中去操作**

### redux-saga



## react-redux

Provider：提供器

Connect：连接器

* Provider：提供器

  用于包裹组件，被包裹的组件/标签都可以访问到store中的内容

  store是Provider中的属性，用于指定仓库

  ```jsx
  import { Provider } from 'react-redux'
  import store from 'store'
  import TodoList from './TodoList'
  const App=(
  	<Provider store={store} >
          <TodoList />
      </Provider>
  )
  ReactDOM.render(App,document.querySeletor("#root"))
  ```

* Connect：连接器

  用于连接，哪个组件需要连接在哪个组件中引入，有了连接器，暴露的值就不直接是组件本身，而是连接器Connect这个方法

  **connect方法接受两个参数：mapStateToProps和mapDispatchToProps。它们定义了 UI 组件的业务逻辑。前者负责输入逻辑，即将state映射到 UI 组件的参数（props），后者负责输出逻辑，即将用户对 UI 组件的操作映射成 Action。**

  语法：connect(映射关系【使用方法】**mapStateToProps**，null【没有】**mapDispatchToProps**)(组件)

  把App中的值进行映射，把状态state映射成属性

  ```jsx
  import React,{ Component } from 'react'
  import { connect } from 'react-redux'
  class App extends Component{
      render(){
          return (
          	<div>
              	<input 
                      value={this.props.inputValue} 
                   	onChange={this.props.changeInput}	   
                   />{/*这里就需要改为props*/}
              </div>
          )
      }
  }
  //把状态state映射成属性props
  const stateToprops=(state)=>{  
      return {
          inputValue:state.inputValue
      }
  }
  
  const dispatchToprops=(dispatch)=>{
      return {
          changeInput(e){
              let action = {
                  type:'CHANGE_INPUT',
                  value:e.target.value
              }
              dispatch(action)
          }
      }
  }
  
  
  export default connect(stateToprops,dispatchToprops)(App)
  ```


## 路由

使用到react-router-dom

```
npm i react-router-dom
```

两种Router

* BrowerRouter  localhost:3000
* HashRouter     localhost:3000/#/

配置：index.js

把Router包裹在最顶层，如果里面还有需要嵌套的项可以放在Router中。**最顶级文件才需要引入Router**

```jsx
import { BrowerRouter as Router } from 'react-router-dom'
import { render } from 'react-dom'
import React from 'react'
import App from './App'
render(
    <Router>
    	<App />
    </Router>,
    document.querySeletor("#root")
)
```

### BrowserRouter与HashRouter的区别

`<BrowserRouter>`：使用 HTML5 提供的 history API 来保持 UI 和 URL 的同步；    不可以通过地址栏手动改变

`<HashRouter>`：使用 URL 的 hash (例如：window.location.hash) 来保持 UI 和 URL 的同步；   显示#     可以通过地址栏手动改变，不太安全   兼容老浏览器

### Route

使用Route组件可在其`path`属性与某个`location`匹配时呈现一些UI，route是非完全匹配

```jsx
import { HashRouter as Router,Route } from 'react-router-dom'

render(
	<Router>
    	<Route component={App} path="/" />
    </Router>
)
```

Route有三种渲染方式

1. `<Route component>`
2. `<Route render>`
3. `<Route children>`

三种渲染方式都将体工相同的三个路由属性

1. match
2. location
3. history

#### component

使用`component`时，Router将根据指定的组件，使用`React.createElement`创建一个新的`React`元素。这意味着如果向`component`提供一个内联函数，那么每次渲染都会创建一个新组件。这将导致现有组建的卸载和新组件的安装，而不仅仅更新现有组件。当使用内联函数进行内联渲染时，使用`render`或`children`

* 可在子组件中直接获取到路由的内容，使用{this.props}

#### render:func

使用`render`可以方便的进行内联渲染和包装，无需进行上文解释和不必要的组件重装。

可以传入一个函数，在位置匹配时调用，而不是使用`component`创建一个新的React元素。`render`渲染方式接收所有与`component`方式相同的`route props`

* 是一个方法，可以传入属性，

  ```jsx
  <Route render={(routeProps)=>{
      console.log(routeProps)//可以直接打印出路由的内容
  	return <HOME x={1} />//传入属性x
  }}></Route>
  
  <Route render={(routeProps)=>{
  	return <Home {...routeProps} x={1} />//可以获取路由的内容以及传入的属性
  }} >
  </Route>
  ```

  

#### children:func

有时候不论`path`是否匹配位置，都想要渲染一些内容。在这种情况下，你可以使用`children`属性。除了不论是否匹配它都会被调用以外，它的工作原理与`render`完全一样

`children`渲染方式接收所有与`component`和`render`方式相同的`route props`，除非路由与URL不匹配，不匹配时`match`为`null`。这允许你可以根据路由是否匹配动态的调整用户界面。

component和render优先于children，因此不要在同一个Route中同时使用多个

### path

用于匹配URL路径

```jsx
<Route component={Home} path="/home" />
//地址栏localhost:300/#/home 出现的内容就是Home组件中的内容
```

### Link

用于跳转，to属性定义跳转目录：一个字符串形式的链接地址，通过 `pathname`、`search` 和 `hash` 属性创建

```jsx
import { Link } from 'react-router-dom'
<li><Link to="./home">首页</Link></li>
```

显式传参

```jsx
<Link to="/article/2?from=article">文章一</Link>
```

隐式传参

```jsx
<Link to={{
        pathname:'/article/2',
        state:{
            form:'article'
        }
}}>文章二</Link>
```



### NavLink

一个特殊版本的 `<Link>`，它会在与当前 URL 匹配时为其呈现元素添加样式属性。

```jsx
import { NavLink as Link } from 'react-router-dom'
<li><Link to="/home">首页</Link></li>
```

被激活的时候会有一个`class="active"`属性

```html
<a aria-current="page" class="active" href="#/home">首页</a>
```

### exact:bool

如果为 `true`，则只有在 `path` 完全匹配 `location.pathname` 时才匹配。

### `<Redirect />`

会导航到一个新的位置。新的位置将覆盖历史堆栈中的当前条目，例如服务器端重定向

to【string】：所有要使用的URL参数必须由`from`提供

from【string】：所有匹配的URL参数都会提供给`to`，必须包含在`to`中用到的所有参数，`to`未使用的其他参数将被忽略

### `<Switch>`

用于渲染与路径匹配的第一个子`<Route>`或`<Redirect>`，相反，仅仅定义一系列`<Route>`时，每一个与路径匹配的`<Route>`都会将包含在渲染范围内，如果想要只选择一个`<Route>`来呈现。比如我们之相匹配`/home`而不匹配其他的，我们就需要用到`<Switch>`

**组件本身渲染，组件内部没有渲染**

```jsx
import { Switch,Route } from 'react-router-dom'

<Switch>
   <Route component={Home} path="/home" />
   <Route component={Article} path="/article" />
   <Route component={Users} path="/users" />
   <Redirect to="/home" />
</Switch>
```

### 高阶组件：withRouter

`withRouter`不像React Redux那样订阅位置更改`connect`来进行状态更改。而是在位置更改后从``组件传播出来，然后重新渲染。这意味着，`withRouter`它**不会**对路线的转变重新呈现，除非它的父组件重新呈现。

静态方法和属性：

包装组件的所有非特定于反应的静态方法和属性将自动复制到“已连接”组件。



只有Route组件渲染的才有props属性，如果向访问Router中的API，就需要使用到withRouter

src/component/BackHome/index.js

```jsx
import React, { Component } from 'react'
import { withRouter } from 'react-router-dom'

class BackHome extends Component {
    clickBtn=()=>{
        // this.props.history.push('/home')
        this.props.history.push({
            pathname:'/home',
            state:{
                id:this.props.match.params.id
            }
        })
    }
    render() {
        console.log(this.props)
        return (
            <button onClick={this.clickBtn} >返回首页</button>
        )
    }
}

export default withRouter(BackHome)
```



### 编程式导航

例子：返回首页

```jsx
export default class ArticleDetail extends Component {
    clickBtn=()=>{
        // this.props.history.push('/home')   方式一
        this.props.history.push({			//方式二
            pathname:'/home',
            state:{
                id:this.props.match.params.id
            }
        })
    }
    render() {
        console.log(this.props)
        return (
            <div>
                文章详情{this.props.match.params.id}
                <button onClick={this.clickBtn}>返回首页</button>
            </div>
        )
    }
}
```



### react路由传参方式



```

```

### 动态路由

1. **通过this.props.match.params.id获取**

detail/index.js

```js
componentDidMount(){
	this.props.getDetail(this.props.match.params.id)
}
const mapDispatch = (dispatch) => ({
	getDetail(id){
		dispatch(actionCreators.getDetail(id))//请求id
	}
})
```

home/components/List.js

```js
{
	list.map((item,index)=>(
		<Link key={index} to={"/detail/"+item.get('id')}>
        //获取id值
        	<ListItem>
        		<img className='pic' src={item.get('imgUrl')} alt="" />
                 <ListInfo>
                    <h3 className="title">{item.get('title')}</h3>
				   <p className="desc">{item.get('desc')}</p>
                 </ListInfo>
        	</ListItem>
         </Link>
	))
}
```

detail/store/reducer.js

```js
export const getDetail = (id) => {
	return (dispatch) => {
		axios.get("/api/detail.json?id="+id).then(res=>{
            //发送id值
			const result = res.data.data;
			dispatch(changeDetail(result.title,result.content))
		})
	}
}
```

App.js

```js
            <Provider store={store}>
                <Router>
                    <div>
                        <Header />
                        <Route path="/" component={Home} exact />
                        <Route path="/detail/:id" component={Detail} exact />
                            //设置id值
                    </div>
                </Router>
            </Provider>
```

2.this.props.loaction.search

## 埋点

概念：埋点分析，是网站分析的一种常用的数据采集方法。

发送数据三种方式：

1. ajax

2. img

   ```
   const img = new Image()
   img.src="http://www.domainname.com/button-01.gif?x=1&y=2"
   ```

3. sendBeacon

## 无状态组件

使用无状态组件可以提高网页的性能，无状态组件的标准只有UI没有业务逻辑

## 组件创建及区别

1. 组件复用
2. 生命周期
3. this指向

## immutable

immutable是Facebook团队提供的一个库，使用immutable库生成的immutable对象是不可直接赋值的对象，它可以有效的避免错误赋值的问题

安装

```
npm install immutable
```

将JS对象转成immutable对象

```
import { fromJS } from 'immutable'
const defaultState = fromJS({
	todoList:[]
})
```

获取属性

```
state.get('todoList');获取store中的todoList
state.get(['Main','todoList']);获取Main组件中store的todoList
```

改变属性：**immutable对象的set方法会结合之前immutable对象的值和设置的值返回一个全新的对象**

```
state.set('todoList',action.value)
```

## dva

全局安装

```
npm install -g dva-cli
```

新建项目

```
dva new 项目名
```

进入项目

```
cd 项目名
```

开启项目

```
npm start
```

### 项目结构

* mock文件夹下的文件用于mock数据的
* public文件夹下是html文件
* src文件夹是我们项目的主要核心代码。包含以下内容
  * index.js和index.css文件：默认的入口和样式文件
  * router.js前端项目的路由入口
  * routes文件包含了每个主页面
  * components文件夹包含了组成页面的Component元素
  * services文件夹中通常包含一些Action，及包含request的请求等
  * models文件夹模型数据的管理位置，用于数据相关的管理
  * utils文件夹包含了一些公用方法，例如request请求等
  * assets文件夹包含了一些静态资源文件，例如图片等

### dva特性

* 仅有5个API
* 支持HMR
* 支持SSR（ServerSideRender）
* 支持Mobile/ReactNative
* 支持TS
* 支持路由和Model的动态加载
* 完善的语法分析库dva-set

![](https://i.loli.net/2020/06/02/lLCk6ovhRWUcbpP.png)

### API

* `app = dva(Opts)`：创建应用，返回dva实例
* `app.use(Hooks)`：配置hooks或者注册插件
* `app.model(ModelObject)`：注册model
* `app.router(Function)`：注册路由表
* `app.start([HTMLElement],opts)`：启动应用

### dva的8个基础概念

* State
* Action
* Model
  * Reducer
  * Effect
  * Subscription
* Router
  * RouteComponent

### 数据流向

数据的改变发生通常是通过用户交互行为或者浏览器行为（如路由跳转等）出发的，当此类行为会改变数据的时候可以通过dispatch发起一个action，如果是同步行为会直接通过Reducers改变State，如果是异步行为（副作用）会先触发Effects然后流向Reducers最终改变State，如果在dva中，数据流向非常清晰简明，并且思路基本跟开源社区保持一致。

## 使用@配置绝对路径

使用`npm eject`暴露配置，目录下会有一个config文件夹下有一个`webpack.config.js`文件，使用搜索：`alias`

```
alias:{
	'@':paths.appSrc,
	'react-native':'.........',
	'.....':'......'
}
```

配置成功后意味着@代表着src目录，所有的路径都是以@为起点

例如：

```
import City from '@/page/city'
```

意为：src下的page下的city

## 27. 使用Charles实现本地数据mock

Tools---Map Local---Add---Protocol(http)---Host(localhost.charlesproxy.com)---Port(3000)---Path(写在axios中设置的url路径)---Local Path(选择json文件所在的路径)---OK--Enable Map Local 与新添加的地址都打上对勾---OK

进入页面刷新---F12---NetWork---点击json文件---Response(显示值)

请求规则：只要访问设置的地址，就会把Local path中的文件返回给你

```js
componentDidMount(){
	axios.get('/api/todolist')
    	.then((res)=>{
        	this.setState(()=>{
                return {
                    list:res.data
                }
            });
    	})
    	.catch(()=>{alert("error")})
}
```

```js
//简写
this.setState(()=>({
    list:[...res.data]
}))
```

## 29. React的CSS过渡动画

通过引入css文件，以及变换state的内容

```jsx
import React,{ Component,Fragment } from 'react';
import './style.css';
class App extends Component {
    constructor(props){
        super(props);
        this.state={
            show:true
        }
        this.handleToggle=this.handleToggle.bind(this);
    }
    render(){
        return (
            <Fragment>
                <div className={this.state.show ? 'show' :'hide'}>hello</div>
                <button onClick={this.handleToggle}>toggle</button>
            </Fragment>   
        )
    }
    handleToggle(){
        this.setState({
            show:this.state.show ? false :true
        })
    }
}
export default App;
```

## 30.  react中使用css动画效果

```css
.show{
    animation: show-item 2s ease-in forwards;
}
.hide{
    animation: hide-item 2s ease-in forwards;
}
@keyframes show-item {
    0%{
        opacity:0;
        color:red;
    }
    50%{
        opacity:0.5;
        color:green;
    }
    100%{
        opacity:1;
        color:blue;
    }
}

@keyframes hide-item {
    0%{
        opacity:1;
        color:red;
    }
    50%{
        opacity:0.5;
        color:green;
    }
    100%{
        opacity:0;
        color:blue;
    }
}
```

## 31. react-transition-group

在github上搜索`react-transition-group`找到第一个，在README中找到`Main Documentation`然后在`Components`中找到`CSSTransition`，里面就是文档示例

使用yarn进行`react-transition-group`的安装

```
yarn add react-transition-group
```

引入到需要使用`react-transition-group`的组件中

```
import {CSSTransition} from 'react-transition-group'
```

使用`<CSSTransition>`标签将需要使用过渡的标签包裹起来，它会自动的给里面的标签加一些内容，

```jsx
<CSSTransition
	in={this.state.show}//在何时增加样式,改变状态的时刻  感知目前是入场状态还是出场状态
    timeout={1000}//动画执行时间
    classNames='fade'//要与css中的fade前缀一致
    unmountOnExit //动画结束后DOM也消失，动画出现DOM也出现
    onEntered={(el)=>{el.style.color='blue'}}  //react-transition-group提供的钩子,在入场动画执行完毕之后给el也就是CSSTransition标签中包裹的div加上color属性为blue
    appear={true}  //此动画第一次展示在页面上也要动画效果（刷新后）【需要在.fade-enter之后添加.fade-appear，以及.fade-enter-active后添加.fade-appear-active】
>
	<div>hello</div>
</CSSTransition>
```



- `fade-appear`，`fade-appear-active`，`fade-appear-done`			出现
- `fade-enter`，`fade-enter-active`，`fade-enter-done`                 进入
- `fade-exit`，`fade-exit-active`，`fade-exit-done`                      退出



当动画执行入场动画的第一个时刻(即刚要执行，但还未执行)，CSSTransition会往div上挂载一个样式，样式的名字为`.fade-enter`

```css
.fade-enter{
	opacity:0;
}
```

当动画执行入场动画的第二个时刻，到入场动画执行完之前的时刻，`.fade-enter-active`

```css
.fade-enter-active{
	opactiy:1;
    transition:opacity 1s ease-in;
}
```

当整个入场动画完成之后，`.fade-enter-done`会被挂载

```css
.fade-enter-done{
	opacity:1;
}
```

出场动画执行的第一个时刻，`fade-exit`

```css
.fade-exit{
	opacity:1;
}
```

出场动画执行的过程中，`fade-exit-acitve`

```
.fade-exit-active{
	opacity:0;
	transition:opacity 1s ease-in;
}
```

整个出场动画执行完成之后，`fade-exit-done`

```
.fade-exit-done{
	opacity:0;
}
```

## 32.实现多个DOM元素动画切换

引入`TransitionGroup`组件，需要两者的配合

```
import {CSSTransition,TransitionGroup} from 'react-transition-group'
```

```jsx
<TransitionGroup>//外层使用TransitionGroup
      {
            this.state.list.map((item,index)=>{
                 return (
                     //在具体的标签里需要使用CSSTransition标签
                     <CSSTransition
                         //不再需要in属性
                        timeout={1000}
                        classNames='fade'
                        unmountOnExit
                        onEntered={(el)=>{el.style.color='blue'}}
                        appear={true}
                        key={index}
                      >
                   	  <div >{item}</div>
                   </CSSTransition>
               )
           })
       }
</TransitionGroup>
```























