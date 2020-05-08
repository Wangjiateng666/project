## 1. 工程目录文件简介

* ServiceWorker	PWA（通过网页写手机app）上线到https协议的服务器上  需要联网才能访问，即便第二次访问时断网也可以访问
* App.test.js	自动化的测试文件
* manifest.json       
* index.js    整个项目的入口文件

![Snipaste_2020-05-02_09-46-50](https://i.loli.net/2020/05/03/CK4M78irgxwI53A.png)

## 2. react中的组件

分为函数组件和类组件

* 函数

```jsx
function welcome(props){
	return <h1>Hello,{props.name}</h1>
}
```

* class

```jsx
class welcome extends React.Component{
	render(){
		return(
			<h1>hello,{this.props.name}</h1>
		)
	}
}
```

通常引入的就是一个组件

必须要引入react，否则无法编译JSX语法

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

## 3. JSX语法

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

## 4. React中的响应式设计思想和事件绑定

不操作DOM而是操作数据

使用变量的时候需要使用`{}`括起来

```jsx
<input value={this.state.inputValue} />
```

绑定事件react：on后的单词首字母要大写

```jsx
<input value={this.state.inputValue} onChange={this.handleInputChange.bind(this)} / >
```

改变`constructor`中的状态使用`setState()`方法向里面传入对象的形式来改变，**`setState`是异步的（为了提升react底层的性能）**

```jsx
handleInputChange(e){
	this.setState({
		inputValue:e.target.value;
	})
}
```

## 5. TODOLIST新增删除

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

## 6. JSX语法细节点

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
<li dangerouslySetInnerHTML={{__html: item}}></li>
//在__html这个属性中写要不转义的内容
```

例如：输入`<h1>内容</h1>`会被写成`h1`标签的格式

### `label`标签中的`for`属性

`react`会认为`for`是指循环，所以发生同名冲突，于是`react`中`label`标签的`for`是`htmlFor`，如果写成`for`会有一个警告

```jsx
<label htmlFor="insertArea"></label>
```

## 7. 拆分组件与组件之间传值

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

## 8. Todolist代码优化

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

### setState参数

setState中可以添加一个参数：`prevState` (修改数据之前的那一次的数据)，可以避免修改state的状态

```jsx
handleBtnClick(){
	this.setState((prevState) => ({
		list:[...prevState.list, prevState.inputValue],
		inputValue:''
	}))
}
```

## 9. 单向数据流

父组件可以向子组件传值，但是子组件不能直接的去改变的值

例如：在一个组件中修改了值，在其他的组件中也使用了这个值，所以其他的组件也会跟着变，一旦出现bug，会给调试带来很大的麻烦

### 解决方法

父组件传递给子组件一个方法，在子组件中调用父组件传递的方法，然后去做修改，实际上是父组件的方法对数据进行改变的

## 10. PropTypes和DefaultProps

### PropTypes

强校验——限制传值的类型

```jsx
TodoItem.propTypes = {
	content: PropTypes.string, //必须为字符串
	deleteItem: PropTypes.func,	//必须是一个function
	index: PropTypes.number, //必须是一个数字
    test:PropsTypes.string.isRequired //必须是一个字符串且必须由父级传递（不为空） 
}
```

### DefaultProps

默认传输——为空时传

```jsx
TodoItem.defaultProps = {
	test:"hello world"
}
```

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

## 11. Props,State与render函数

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

## 12. 虚拟DOM

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

## 13. 深入了解虚拟DOM

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

## 14. 虚拟DOM中的Diff算法

`Diff`全称`diffrence`

### 同级比较

同层比对，对一层DOM比较，如果一致，比较第二层，如果不一致，react就不会继续往下比较，于是把原始页面上的虚拟DOM对应下面所有的节点的DOM全部删除，重新生成一遍下面所有的节点的DOM，然后用重新生成的节点的DOM去替换原始页面上的DOM

同级比较，算法会简单，且速度会很快，尽管可能会造成DOM重新渲染上的浪费，但他大大减少了两个虚拟DOM在比对上的性能消耗

### setState()

`setState`可以把多次对`setState`的修改合并为一次，减少对虚拟DOM修改的次数

### 不要使用index作为key值

**引入key值实际上是为了提高虚拟DOM比对的性能**

通过Todolist添加了三个列表项，分别为a、b、c，他们的index值：a-0，b-1，c-2，这个时候删除a，他们的index值就会发生变化：b-0，c-1 。以前的b和现在的b无法建立起关系，key值就不稳定，key值也就失去了意义。

解决：

可以使用他的值作为key值，尽量要使用一个稳定的值

例如：a-a，b-b，c-c。删除a，b依旧对应b，c依旧对应c

## 15. React中ref的使用

### ref

允许我们访问 `DOM `节点或在 `render` 方法中创建的 `React `元素。

获取触发事件的元素对应的`DOM`

使用场景：

* 管理焦点，文本选择或媒体播放
* 触发强制动画
* 集成第三方DOM库

Refs 是使用 `React.createRef()` 创建的，并**通过 `ref` 属性附加到 React 元素**。在构造组件时，通常将 Refs 分配给实例属性，以便可以在整个组件中引用它们。

```jsx
<input ref={(input) => {this.input=input}} />
```

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

## 16. 生命周期

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

组件被更新之前，他会自动被执行

语法：`shouldComponentUpdate(nextProps,nextState)`

```js
shouldComponentUpdate(){//是否需要更新你的组件？
	return true;	//如果是false则不更新
}
```

如果`retrun false`那么后面整个的流程都不会进行

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

### componentWillUnmount()

当这个组件即将被从页面中剔除的时候，会自动执行

## 17. 生命周期的使用场景

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

### Ajax

`react`中的`Ajax`会被放在`componentDidMount()`中，之所以不能放在`render`中就是因为`render`这个函数会反复的执行，只要数据发生变化就会执行，从而造成死循环。而`componentDidMount()`在组件被挂载到页面上的时候，会执行一次。之后不会被重新的执行

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

## 18.使用Charles实现本地数据mock

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



## 19. React的CSS过渡动画

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

## 20.  react中使用css动画效果

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

## 21. react-transition-group

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

## 22.实现多个DOM元素动画切换

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























