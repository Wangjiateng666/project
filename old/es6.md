# ES6

在react与vue中使用的都是ES6

## Babel转换器

老的浏览器只能支持ES5不支持ES6，所以需要安装转换器把ES6转换成ES5从而在浏览器中运行，转换器的名字：Babel转换器

```
babel-loader:把es6转换为es5
```

## ES6新增

1. 变量的创建：let，const
2. 解构赋值：数组，对象
3. 对象、函数、数组、字符串的扩展
4. 两个数据结构
5. 异步：三个
6. 创建对象的方式
7. 对象继承的方式

## 1. 变量let和const

### let

var：全局变量、局部变量-->变量的提升

es6中新增了块级作用域，只能在当前的作用域范围之内进行使用

```js
{
    let a=10;
    var b=20;
}
console.log(a);//报错
console.log(b);//20
```

* 声明变量的

* 不会污染全局变量

* 不存在变量提升

* 不能在相同作用于下重复声明

* 暂时性死区（使用let声明之前，变量是无法使用的）

  ```js
  console.log(a);
  //这之前是暂时性死区
  let a=10;
  ```

### const

const实际上保证的不是变量的值不能变，而是变量指向的那个内存地址所保存的数据不得改动

* 用来声明常量
* 值一旦声明不允许修改
* 只能进行读取
* 暂时性死区
* 不可重复声明

### var，const，let区别

```
var:可以创建局部和全局变量，变量会进行提升
let:声明的是变量、没有声明不允许使用、不能进行多次声明
const:声明的是常量，只能读取不能修改

let,const:存在块级作用域，出了作用域就没办法获取和使用
```

### 块级作用域

ES5不使用块级作用域可能出现的问题

* 内层变量会覆盖外层变量
* 用来计数的循环变量泄露为全局变量

ES6中的块级作用域

* 下面的两个n属于两个不同作用域，不会彼此影响

```js
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
```

* 允许块级作用域的任意嵌套

```js
{{{{
	{let insane='hello world'}
	console.log(insane);//报错，因为不在一个作用域无法读取，每层都是单独的作用域
}}}}
```

* 使匿名立即执行函数表达式不再必要了

```js
//匿名
(function(){
    var temp=...;
    ...
}());
//块级作用域写法
{
    let tmp=...;
    ...
}
```

### 块级作用域与函数声明

* 允许在块级作用域内声明函数
* 函数声明类似于var，即会提升到全局作用域或函数作用域的头部
* 同时，函数声明还会提升到所在块级作用于的头部

### ES6声明变量的六种方法

1. var
2. let
3. const
4. function
5. import
6. class

### 顶层对象的属性

顶层对象，在浏览器环境指的是`window`对象，在node中指的是`global`对象，ES5中，顶级对象的属性与全局变量是等价的

```js
window.a=1;
a	//1

a=2;
window.a	//2
```

* var和function：声明的全局变量依旧是顶层对象的属性
* let，const，class：声明的全局变量，不属于顶层对象的属性

```js
var a=1;
window.a;//1

let b=1;
window.b;//undefined
```

## 2. 变量的解构赋值

按照一定的模式，从数组和对象中提取值，对变量进行赋值，被称为解构

### 数组的解构赋值

数组的元素是按次序排列的

```js
let a=10;//之前创建变量的方式
let b=20;
let c=30;

let [a,b,c]=[10,20,30];//这种形式称为解构赋值
```

如果解构不成功，值就是undefined

```js
let [a,b,c]=[10,20];
console.log(c);//undefined
```

其他形式

```js
let [a,...b]=[10,20,30];
console.log(b)//[20,30]会把后面的所有值都给b
```

```js
let [ , ,third]=["foo","bar","baz"];
console.log(third) //"baz"
```

```js
let [x, ,y]=[1,2,3];
console.log(x,y);//1  3
```

```js
let [x, y, ...z] = ['a'];
console.log(x) // "a"
console.log(y) // undefined
console.log(z) //[]
```

解构赋值过程中允许有默认值，默认值只有在undefined的时候才有效

```js
let [a,b='q']=[10,undefined];
console.log(b);//q
不写前面的默认值的话就是undefined
```

### 对象的解构赋值

对象不按照次序，对象是变量必须与属性同名，才能取到正确的值

```js
let {a,b}={a:"123",b:"234"}
console.log(a)//123
```

如果变量名与属性名不一致，必须写成下面这样

```js
let {foo:baz}={foo:'aaa',bar:'bbb'};
console.log(baz) //"aaa"

let obj={first:'hello',last:'world'};
let {first:f,last:l}=obj;
console.log(f); //'hello'
console.log(l); //'world'

let {foo:foo,bar:bar}={foo:'aaa',bar'bbb'};
//对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。

let {foo:baz}={foo:"aaa",bar:"bbb"};
console.log(baz); //"aaa"
console.log(foo); //error: foo is not defined
//真正被赋值的是变量baz，不是模式foo

let obj={
    p:[
        'hello',
        {y:'world'}
    ]
};
let {p:[x,{y}]}=obj;//这里面的p是模式不是变量，除非是这种let {p,p:[x,{y}]}=obj;
console.log(x) //'hello'
console.log(y) //'world'
```

变量中存在没有赋值的，返回也是undefined

```js
let {a,b,c}={a:"123",b:"234"}
console.log(c)//undefined
```

可以指定默认值与数组的生效条件一样，对象的属性值严格等于undefined时

```js
var {x=3}={x:undfined};//3
var {x=3}={x:null};//null，因为不严格相等于undefined
```

#### 注意点

1. 如果要将一个已经声明的变量用于解构赋值，必须非常小心

   ```js
   let x;
   ({x}={x:1});
   //JavaScript引擎会将{x}理解成为一个代码块，从而会发生语法错误，所以需要使用圆括号放在一起
   ```

2. 解构赋值允许等号左边的模式之中，不放置任何变量名。因此，可以写出非常古怪的赋值表达式。

   ```js
   ({}=[true,false]);
   ({}='abc');
   ({}=[]);
   //表达式没有意义，但是合法，可以执行
   ```

3. 由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构。

   ```js
   let arr=[1,2,3];
   let {0:first,[arr.length-1]:last}=arr;
   console.log(first);//1
   console.log(last);//3
   //arr.length=3   3-1=2   arr[2]=3
   ```

### 字符串的解构赋值

```js
const [a,b,c,d,e]="hello";
a//"h"
b//"e"
c//"l"
d//"l"
e//"o"
```

类似数组的对象都有length属性，因此还可以对这个属性解构赋值

```js
let {length:len}='hello';
console.log(len)//5
```

### 函数参数的解构赋值

```js
function add([x,y]){
    return x+y;
}
add([1,2]);//3
```

```js
[[1,2],[3,4]].map(([a,b])=>a+b);
// [3,7]
```

变量的解构赋值最多的用法：

* 变量交换

```js
let x=1;
let y=2;
[x,y]=[y,x]; //x=2,y=1;
```

* 从函数返回多个值

```js
//返回一个数组
function ex(){
    return [1,2,3];
}
let [a,b,c]=ex();
//返回一个对象
function ex(){
    return{
        foo:1,
        bar:2
    };
}
let {foo,bar}=ex();
```

* 函数参数的定义

```js
// 参数是一组有次序的值
function f([x, y, z]) { ... }
f([1, 2, 3]);

// 参数是一组无次序的值
function f({x, y, z}) { ... }
f({z: 3, y: 2, x: 1});
```

* 提取json数据

```js
let jsonData={
	id:42,
    status:"ok",
    data:[867,5309]
};
let {id,status,data:number}=jsonData;
console.log(id,status,number);
//42,"OK",[867,5309]
```

## 3. 字符串的扩展

### JSON.stringify()

为了确保返回的是合法UTF-8字符，ES2019改变了JSON.stringify()的行为。如果遇到`0xD800`到`0xDFFF`之间的单个码点，或者不存在的配对形式，它会返回转义字符串，留给应用自己决定下一步的处理。

```js
JSON.stringify('\u{D834}') // ""\\uD834""
JSON.stringify('\uDF06\uD834') // ""\\udf06\\ud834""
```

### 模块字符串

```js
$("#result").append(
	`
	There are<b>${basket.count}</b>itemes in your basket,<em>${basket.onSale}</em>are on sale!
	`
);
```

## 4. 字符串的新增方法

### includes(),startsWith(),endsWith()

es5中只有indexOf()

返回的都是布尔值（true/false）

* includes()：是否包含某个字符串
* startsWith()：是否以什么开头
* endsWith()：是否以什么结尾

* (str，index)：

  str：代表要检测的字符串是谁

  index：从索引为几开始检索

### repeat()

会返回一个新字符串，是原字符串重复几次的结果

用法：string.repeat(n)：n代表重复次数

```js
console.log("123".repeat(3))
//123123123
```

n如果是小数会进行向下进行取整

```js
console.log("123".repeat(3.8))
//123123123
```

n如果是0到-1之间的小数，则等同于0

n如果是NaN也等同于0

### padStart(在字符串前追加)、padEnd(在字符串后追加)

在字符串前/后追加

```js

padStart(追加完成后字符的个数,"需要追加的字符")

console.log("123".padStart(5,"ab"))
//ab123 
//如果长度不够则重复将需要追加的内容进行追加 例如：6的话，aba123
```

### trimStart(),trimEnd()

去除前/后空格

## 正则的扩展

### RegExp构造函数

es5：new RegExp('abc','i')

es6：new RegExp(/abc/,'i')

#### RegExp.prototype.flags属性

ES6为正则表达式新增了flags属性，会返回正则表达式的修饰符

```js
//ES5的source属性
//返回正则表达式的正文
/abc/ig.source
//"abc"

//ES6的flags属性
//返回正则表达式的修饰符
/abc/ig.flags
//"gi"
```

## 数值的扩展

### Number.parseInt()，Number.parseFloat()

在ES5中：parseInt()和parseFloat()都是全局函数，但是在ES6中移植到了Number对象中，所以在使用ES6的时候必须：

```js
Number.parseInt();
Number.parseFloat();
```

### Number.isInteger()

用来判断一个数值是否为整数，布尔值

```js
Number.isInteger(25) //true
Number.isInteger(25.0) //true
Number.isInteger(25.1) //false
//如果不是数值，返回false
```

### Math.trunc()

取整，返回的是整数部分，无论正负都是如此

### Math.sign()

用来判断一个数到底是正数、负数、还是零。对于非数值，会先转会为数值

* 参数为整数，返回+1
* 参数为负数，返回-1
* 参数为0，返回0
* 参数为-0，返回-0
* 其他值，返回NaN

## 函数的扩展

### 函数的默认值

```js
function test(a,b="world"){
	console.log(a+v)
}
test("hello ");
//创建形参的时候赋一个值就是默认值
如果想要给函数的参数设置默认值，当传的实参没有被赋值的时候会用到默认值
```

* 参数在默认声明的情况下，是不允许使用let或const创建的
* 参数有默认值的话，函数不能有同名参数，参数与参数不能同名

es5中函数length属性代表的是形参的个数

es6中length属性代表没有默认值的形参个数，只要遇到有默认值的就会失效

```js
function test(a,b="world",c){
	console.log(test.length);//1
}
function test(b="world",a,c){
    console.log(test.length);//0
}
```

### 与解构赋值默认值结合使用

```js
function foo({x,y=5}){
	console.log(x,y);
}
foo({}) //undefined 5
foo({x:1})	//1 5
foo({x:1,y:2})	//2 2
foo() //报错
```

上面的代码使用了对象的解构赋值默认值，没有使用函数参数默认值。只有当函数`foo`的参数是一个对象时，变量`x`和`y`才会通过解构赋值生成。如果函数`foo`调用时没体工参数，变量`x`和`y`就不会生成，从而报错。通过提供函数参数的默认值，就可以避免这种情况。

```js
function foo({x,y=5}={}){
	console.log(x,y);
}
foo() // undefined 5
```

如果没有提供参数，函数foo的参数默认为一个空对象

```js
function fetch(url,{body='',method='GET',headers={}}){
    console.log(method);
}
fetch('http://www.1.com',{})//"GET"
fetch('http://www.1.com')//报错
```

第二个参数是对象，可以为三个属性设置默认值，但是上面这种写法不能省略第二个参数，如果结合函数参数的默认值，就可以省略第二个参数，也就出现了双重默认值

```js
function fetch(url,{body="",method="GET",headers={}}={}){
	console.log(method);
}
fetch('http://www.1.com')//"GET"
```

由于fetch没有第二个参数，函数参数默认值会生效，其次是解构赋值的默认值

```js
function fetch(url,{body="",method="",header={}}={method:"POST"}){
    console.log(method);
}
fetch('http://www.1.com');//"POST"
```

```js
//写法一
function m1({x=0;y=0}={}){
    return [x,y];
}
//写法二
function m2({x,y}={x:0,y:0}){
    return [x,y];
}
```

两种写法都对函数的参数设定了默认值，区别是写法一函数参数默认值是空对象，但是设置了对象解构赋值的默认值；写法二函数参数的默认值是一个有具体属性的对象，但是没有设置对象解构赋值的默认值

```js
// 函数没有参数的情况
m1() // [0, 0]
m2() // [0, 0]

// x 和 y 都有值的情况
m1({x: 3, y: 8}) // [3, 8]
m2({x: 3, y: 8}) // [3, 8]

// x 有值，y 无值的情况
m1({x: 3}) // [3, 0]
m2({x: 3}) // [3, undefined]

// x 和 y 都无值的情况
m1({}) // [0, 0];
m2({}) // [undefined, undefined]

m1({z: 3}) // [0, 0]
m2({z: 3}) // [undefined, undefined]
```

### 作用域

一旦设置了参数的默认值，函数进行声明初始化时，参数会形成一个单独的作用域。

```js
var x = 1;
function f(x, y = x) {
  console.log(y);
}
f(2) // 2
参数y的默认值等于变量x。调用函数f时，参数形成一个单独的作用域。在这个作用域里面，默认值变量x指向第一个参数x，而不是全局变量x，所以输出是2。
```

```js
let x = 1;
function f(y = x) {
  let x = 2;
  console.log(y);
}
f() // 1
函数f调用时，参数y = x形成一个单独的作用域。这个作用域里面，变量x本身没有定义，所以指向外层的全局变量x。函数调用时，函数体内部的局部变量x影响不到默认值变量x。
```

### 参数默认值的应用

```js
function throwIfMissing() {
  throw new Error('Missing parameter');
}

function foo(mustBeProvided = throwIfMissing()) {
  return mustBeProvided;
}

foo()
//Error:Missing parameter
```

foo函数如果调用的时候没有参数，就会调用默认值`throwIfMissing`函数，从而抛出一个错误

### arguments

arguments代表的是实参，在arguments这个对象上返回的值是一个实参数组 ，如果想要获取任意一个实参的话，使用数组方式进行获取，arguments对象不是一个数组，是一个类似数组的对象

### rest参数

rest参数是一个真正的数组，而arguments是一个类似数组的对象并不是数组。

在es6中引入了rest参数（...变量名），

rest参数后面不能再有其他参数的

```js
function test(a,...b){}//正确
function test(a,...b,c){}//错误
```

es6中新增了length属性，length属性是不能获取rest参数的

```js
function test(...values){//...变量名
    for(key of values){
        console.log(key);
    }
}
test(1,3,4,5,7);
```

### 新增遍历数组方法

```js
//for...of
var arr=[1,3,4,5];
for (key of arr){
    console.log(key);//1 3 4 5
}
```

### 严格模式

定义严格模式有两种方式定义：

1. 全局定义：把整个js文件定义为严格模式
2. 局部定义：只在函数内部进行严格模式的定义

```js
'use strict'
function test(a=10){
    'use strict';//只有函数内部进行严格模式的定义
}
```

以下格式无法进行严格模式

* 参数有默认值
* 有rest参数
* 有解构赋值

### name属性

获取的是当前函数的函数名，es6新增

```js
function test(){}
console.log(test.name);//test，字符串格式
```

### 箭头函数

var 函数名=(形参)=>函数体

```js
var foo=v=>v;

//等同于
var foo=function(v){
    return v;
};
```

如果箭头函数不需要参数或需要多个参数，就需要使用一个圆括号代表参数部分

```js
var f=()=>5;

//等同于
var f=function(){
    return 5;
};
```

如果箭头函数的代码块多于一条语句就需要使用大括号将他们括起来，并且使用return语句返回

```js
var sum=(sum1,sum2)=>{ return sum1+sum2;}
```

由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上大括号，否则报错

```js
//报错
let get=id=>{id:id,name:"temp"};
//不报错
let get=id=>({id:id,name:"temp"});
```

箭头函数的好处之一是简化回调函数

```js
// 正常函数写法
[1,2,3].map(function (x) {
  return x * x;
});

// 箭头函数写法
[1,2,3].map(x => x * x);
```

```js
// 正常函数写法
var result = values.sort(function (a, b) {
  return a - b;
});

// 箭头函数写法
var result = values.sort((a, b) => a - b);
```

```js
var test=(...nums)=>nums
console.log(test(1,2,3,4,5))
```

### 不适合箭头函数的情景

* 直接修改this指向的时候
* 在给某个对象添加事件时，处理函数不能使用箭头函数，因为箭头函数中的this代表的是全局对象window，不能指向当前操作对象

### 箭头函数需要注意点

1. 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。
2. 不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误。
3. 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
4. 不可以使用`yield`命令，因此箭头函数不能用作 Generator 函数。

* this指向问题

  普通函数获取prototype是由返回值的：有this

  箭头函数获取prototype返回的是undefined，箭头函数没有prototype原型对象

* 使用箭头函数在继承的时候是谁的this

  正常情况下，如果使用的不是箭头函数的话，那么继承的时候this的指向是会发生变化的，谁里面调用这个函数this指向的就是哪个对象

* 不能直接修改箭头函数的this指向

* 箭头函数中的运算符优先级要比普通函数中的要高

```js
let a,
barObj={msg:"bar的this指向"},
fooObj={msg:"foo的this指向"};
function bar(){
	a=()=>{
		console.log(this)//打印的是当前这个对象
	}
}
function foo(){
	a()
}
bar.call(barObj);//把bar方法集成到barObj对象上，因为箭头函数在继承的时候继承的是第一层上面的this，即箭头函数中this以开始指向的是谁，那么始终指向谁，不管怎么操作this的指向都是不会发生变化
foo.call(fooObj);//把foo方法集成到barObj对象上
```

### 尾调用优化

尾调用是函数式编程的一个重要概念，就是指某个函数的最后一步是调用另一个函数。

```js
function f(x){
	return g(x);
}
//上面代码的最后一步是调用函数g，这就叫做尾调用
```

以下三种都不是尾调用

```js
//一：调用函数g之后还有赋值操作，所以不属于尾调用
function f(x){
	let y=g(x);
	return y;
}
//二：调用后还有操作，即使写在一行内也不属于尾调用
function f(x){
    return g(x)+1;
}
//三
function f(x){
    g(x);
}
//三，等同于
function f(x){
    g(x);
    return undefined;
}
```

尾调用不一定出现在函数尾部，只要是最后一步操作即可。

```javascript
function f(x) {
  if (x > 0) {
    return m(x)
  }
  return n(x);
}
```

函数`m`和`n`都属于尾调用，因为它们都是函数`f`的最后一步操作。

### 尾递归函数

```js
function tailFactorial(n,total){
	if(n===1) return total,
    return tailFactorial(n-1,n*total);
}
console.log(tailFactorial(5,1));//120
```

### 函数柯里化

把接收多个参数的函数转换成接收一个参数的函数（单一的这个参数是多个参数中的第一个）

思想：降低通用性、提高适用性，是一个js预处理思想

特点：

1. 参数的复用上来说：需要输入多个参数，最终转化成只需要一个参数，其余的使用arguments对象获取
2. 避免重复判断一个条件是否符合，不符合的话直接return不再执行
3. 避免重复执行程序，等需要时执行

思路：

* curry方法，就是把myAdd接收3个参数进行转换之后转换成add，add这个方法不在一次性接收3个参数了，而是一个一个的慢慢接收，当参数达到3个了就返回结果
* 这个过程中实际上用到的也是闭包来实现的，我们把接收的参数存到一个对象中，利用闭包让这些参数再函数执行完之后不清缓存的特点来实现
* args是传过来的参数，_args代表的是原本有的参数
* 接下来就是让args和原本有的 _args进行结合，因为再实现柯里化的时候是一个参数传的

```js
let myAdd=(a,b,c)=>a+b+c;
function curry(fn,args){
    let len=fn.length//获取的是形参的个数
    let _this=this;
    let _args=args || [];//因为arguments代表的是实参，有可能船只有可能不传值，如果传值那就是这个参数，否则是空数组
    return function(){
        let args=Array.prototype.slice.apply(argments);//args就是读取myAdd接收的参数
        args=Array.prototype.concat.call(_args,args);
        if(args.length<len){//判断接收的参数是否小于形参的个数，小于的话继续接收，否则直接返回值
            return curry.call(_this,fn,args);
        }
        return fn.apply(this,args);
    }
}
let add=curry(myAdd);
console.log(add(1)(2)(3));
```

```js
let myadd=(a,b,c,d)=>a+b+c+d;
const curry = (fn,...args) => args.length < fn.length // 参数不够长,重新柯里化,等待新的参数
? (...arguments) => curry(fn,...args,...arguments)   // 参数长度足够,执行函数
: fn(...args);
let add=curry(myadd);
console.log(add(2)(3)(1)(5));
```





















