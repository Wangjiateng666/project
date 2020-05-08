# JS高级

## 闭包

是指**有权访问另一个函数作用域中变量的函数.**创建闭包常见的方式,就是在一个函数内部创建另一个内部(私有)函数

<font color=" #f00">闭包的应用：</font>

1. 可以使用闭包进行封装--选项卡、轮播图
2. 如果变量是全局变量的话，在特效里面使用的时候改变这个变量的话，会对全局变量造成污染，使用自调函数包裹起来，这样的话就不会对全局的变量造成污染。
3. 可以进行缓存--为了能让别人进行访问。

想使用闭包使用的是带返回值的函数

函数执行完之后缓存就释放了,所以没有办法找到

带返回值的匿名函数

```javascript
返回一个匿名函数
function test(){
    var x=20;
    return function(){
        return x;
    }
}
var a=test();
alert(a());
```

```javascript
函数在调用的时候对全局变量进行赋值
var y;
function test(){
    var x=20;
    y=function(){
        return x;
    }
}
test();
alert(y());
```

* 什么是闭包？	可以访问函数内部的私有变量，并且还是一个函数

* 第一种直接return 一个匿名函数，把这个匿名函数给全局变量

  第二种，在函数里面对全局变量赋值，赋的这个值是一个匿名函数

  这两个全局变量都是闭包函数


```javascript
function test(arg){
	var y=function(){
		return arg;
	}
	arg++;
	return y;
}
var a=test(123);			/*124*/
alert(a());
```

```js
存的是匿名函数，所以每次都return i，for循环执行到3结束，并且始终都没有执行，所以返回3
a存的是三个匿名函数
function test(){
    var x=[];
    var i;
    for(i=0;i<3;i++){
        x[i]=function(){
            return i;
        }
    }
    return x;
}
var a=test();
alert(a[0]());			/*   3  3  3  返回的不是确切的值，而是每个数组所对应的匿名函数*/
alert(a[1]());
alert(a[2]());
```

```js
function test(){
    var x=[];
    var i;
    for(i=0;i<3;i++){
        x[i]=(function(y){
            return function(){
                return y;
            }
        })(i);
    }
    return x;
}
var a=test();
alert(a[0]());		/*  0  1  2  返回*/
alert(a[1]());
alert(a[2]());
```

```js
不使用自调函数来实现
function test(){
    function name(y){
        return function(){
            return y;
        }
    }
    var x=[];
    var i;
    for(i=0;i<3;i++){
        x[i]=name(i);
    }
    return x;
}
var a=test();
alert(a[0]());
alert(a[1]());
alert(a[2]());
```

## 面向对象封装

```js
var getValue,setValue;
(function(){
    var secret=0;
    getValue=function(){
        return secret;
    };
    setValue=function(v){
        secret=v;
    };
})();
alert(getValue());查看内部局部变量值
setValue(3);设置内部局部变量的值
alert(getValue());
```

## 迭代器

* 传的是一个数组
* 每调用一次值就会发生变化一次

```js
function setup(x){
    var i=0;
    return function(){
        return x[i++];
    }
}
var next=setup(["a","b","c"]);	/* a  b  c  */
alert(next());
alert(next());
alert(next());
```

## 闭包注意事项

```js
function setup(x){
    var i=0;
    return function(){
        return x[i++];
    }
}
var next=setup(["a","b","c"]);	/* a  b  c  */
alert(next());
alert(next());
alert(next());
next=null;
```

闭包会在父函数外部，改变父函数内部变量的值。闭包可以在函数外面改变值

* <font color=" #7FFFAA">闭包</font>：有权访问一个函数内部私有变量的函数

* <font color=" #7FFFAA">实现闭包的方法</font>：

  第一个：直接返回一个匿名函数赋值给一个全局变量

  第二个：直接在函数内部对全局变量进行赋值——赋值内容还是匿名函数

  第三个：使用自调函数返回一个匿名函数，在匿名函数中返回私有变量的值（这个值会随着自调函数的实参的变化而变化的）

* <font color=" #7FFFAA">闭包的应用</font>：
  
  1. 封装——选项卡、焦点图、轮播图
  2. 迭代器——实参是数组
* <font color="#7FFFAA">闭包缺点</font>：
  
  1. 会造成内存泄漏
  2. 会改变函数内部的私有变量的值

## 面向对象程序设计

* 什么是面向对象：面向对象是一种思想，这种思想只注重功能，不注重过程

* 面向对象的特点：聚合

* 创建对象的方法：

  1.原始模式

  2.工厂模式

  3.构造函数

  4.混合模式

  5.Json格式

  ​	json格式的字符串转换成js对象的方法：

  ​		1.eval	2.JSON.parse()

### javascript面向对象程序设计

* <font color="#7FFFAA">面向对象编程特点</font>

  ​	<font color="#ff0">聚合</font>:将所有的内容聚集到一起,生成一个集合

  ​	<font color="#ff0">封装</font>:不考虑内部实现,只考虑提供的功能

  ​	<font color="#ff0">继承</font>:从已有对象继承出新对象

  ​			多重继承

  ​	<font color="#ff0">多态</font>:可以以不同种形式出现

* <font color="#7FFFAA">对象的组成</font>

  ​	属性——变量(静态特性)

  ​	方法——函数(动态行为)

#### 原始模式

创建对象:

缺点：只要需要重新创建一个对象就要重新实例化(new)一次

```js
var 对象名=new Object();
对象名.属性="属性值"；
对象名.方法=function(){};
调用方法：
对象名.属性；
对象名.方法；
```

```js
var person = new Object();
person.name="lily";
person.age=22;
person.talk=function(){
    alert("好好学习");
}
console.log(person.name);
person.talk();
```

#### 工厂模式

创建方法:

采取的是闭包的原理来实现的

首先创建一个方法，在方法里面使用的是原始创建对象的方式实例化出来的对象

闭包的缺点他也存在，内存泄漏

```js
function 方法名 （属性值1，属性值2，...）{
var 对象名=new Object();
对象名.属性="属性值"；
对象名.方法=function(){}
return 对象名；
}
调用方法：
var 对象名=方法名（实参1，实参2，...）；
对象.属性；
对象.方法（）
```

```js
function test(){
    var person=new Object();
    person.name="Lily";
    person.age=19;
    person.talk=function(){
        alert("好好学习");
    }
    return person;
}
var a=test();
console.log(a.name);
a.talk();
```

```js
/*传参*/
function test(name,age,talk){
    var person=new Object();
    person.name=name;
    person.age=age;
    person.talk=function(){
        alert(talk);
    }
    return person;
}
var a=test("tom","20","hello");
console.log(a.name);
a.talk();
var b=test("zs","30","hell1");
console.log(b.name);
```

#### 构造函数

创建方法:

与其他最大的区别就是有没有this

有new的时候才算创建

缺点：this的指向

```js
创建方法
function 方法名（属性值1，属性值2，...）{
this.属性="属性值"；
this.属性="属性值"；
this.方法=function(){};
}
调用方法：
var 对象名=new 方法名(实参1，实参2，...);
```

```js
1.
function Person(){
    this.name="lily";//不写实例化的时候这个this代表的是window
    this.age=23;
    this.talk=function(){
        alert("好好学习");
    }
}
var persona =new Person();
console.log(persona.name);
2./*传参*/
function Person(name,age){
    this.name=name;//不写实例化的时候这个this代表的是window
    this.age=age;
    this.talk=function(){
        alert(this.name);
    }
}
var persona =new Person("tom",23);
console.log(persona.name);
persona.talk();
```

#### 混合模式

创建方法:

```js
创建方法
function 方法名（形参，形参...）{
对象.prototype.属性=属性值；
对象.prototype.方法=function(){};
}
调用方法：
var 对象=new 方法名(实参1，实参2...);
对象名.属性；
对象名.方法
```

```js
function Person(){
    Person.prototype.name="lily";
    Person.prototype.age=23;
    Person.prototype.talk=function(){
        alert("你好");
    }
}
var persona=new Person();
console.log(persona.name);
```

#### json

是一种轻量级的数据交换格式

可以使用他创建对象

属性名：字符串

属性值：字符串、数值、布尔值、函数、数组、对象、null等

对象：对象在js中标识为"{}"括起来的内容，数据结构为{key:value,key:value,key:value}的键值对的结构，在面向对象的语言中，key为对象的属性，value为对应的 

```js
var person={
    "name":"lily",
    "age":30,
    "talk":function(){
        alert("好好学习");
    },
    children:[{
        "name":"TOM",
        "age":2
    },{
        "name":"jerry",
        "age":5
    }]
}
console.log(person.children[1].name);
```

```js
1.
var person='{}';
var jso=eval("("+person+")");//js转换为对象
console.log(jso);

2.
var jso=JSON.parse(person);//json把字符串转化为对象
console.log(jso);
```

## 读取对象的属性

读取对象的属性，有两种方法，一种是使用点运算符，还有一种是使用方括号运算符。

```js
var obj = {
  p: 'Hello World'
};

obj.p // "Hello World"
obj['p'] // "Hello World"
```

上面的代码分别使用点运算符和方括号运算符，读取属性`p`

请注意，如果使用方括号运算符，键名必须放在引号里面，否则会被当做变量处理。

```js
var foo = 'bar';
var obj = {
  foo: 1,
  bar: 2
};

obj.foo  // 1
obj[foo]  // 2
```

上面代码中，引用对象`obj`的`foo`属性时，如果使用点运算符，`foo`就是字符串；如果使用方括号运算符，但是不使用引号，那么`foo`就是一个变量，指向字符串`bar`。

方括号运算符内部还可以使用表达式，数字键可以不加引号，因为会自动转成字符串。但是，数字键名不能使用点运算符因为会被当做小数点，只能使用方括号运算符。

```js
var obj = {
  123: 'hello world'
};

obj.123 // 报错
obj[123] // "hello world"
```

## 1.属性的赋值

点运算符和方括号运算符，不仅可以用来读取值，还可以用来赋值

```js
var obj = {};

obj.foo = 'Hello';
obj['bar'] = 'World';
```

上面代码中，分别使用点运算符和方括号运算符，对属性赋值。

JavaScript 允许属性的“后绑定”，也就是说，你可以在任意时刻新增属性，没必要在定义对象的时候，就定义好属性。

```js
var obj={p:1};
var obj={};
obj.p=1;
```

## 2.属性的查看

查看一个对象本身的所有属性，可以使用`Object.keys`方法

```js
var obj={
	key1:1;
	key2:2
};
Object.keys(obj);
//['key1','key2']
```

## 3.属性的删除：delete命令

`delete`命令用于删除对象的属性，删除成功后返回`true`

```js
var obj = { p: 1 };
Object.keys(obj) // ["p"]

delete obj.p // true
obj.p // undefined
Object.keys(obj) // []
```

上面代码中，`delete`命令删除对象`obj`的`p`属性。删除后，再读取`p`属性就会返回`undefined`，而且`Object.keys`方法的返回值也不再包括该属性。

注意：删除一个不存在的属性，`delete`不报错，而且返回`true`。

```js
var obj = {};
delete obj.p // true
```

上面代码中，对象`obj`并没有`p`属性，但是`delete`命令照样返回`true`。因此，不能根据`delete`命令的结果，认定某个属性是存在的。

只有一种情况，`delete`命令会返回`false`，那就是该属性存在，且不得删除。

```js
var obj=Object.defineProperty({}, 'p',{
	value:123,
	confighurable:false,
})

obj.p;
delete obj.p;
```

上面代码之中，对象`obj`的`p`属性是不能删除的，所以`delete`命令返回`false`（关于`Object.defineProperty`方法的介绍，请看《标准库》的 Object 对象一章）。

另外，需要注意的是，`delete`命令只能删除对象本身的属性，无法删除继承的属性（关于继承参见《面向对象编程》章节）。

```js
var obj={};
delete obj.toString //true
obj.toString //function toString() {[native code]}
```

上面代码中，`toString`是对象`obj`继承的属性，虽然`delete`命令返回`true`，但该属性并没有被删除，依然存在。这个例子还说明，即使`delete`返回`true`，该属性依然可能读取到值。

## 4.属性是否存在：in运算符

`in`运算符用于检查对象是否包含某个属性（注意，检查的是键名，不是键值），如果包含就返回`true`，否则返回`false`。它的左边是一个字符串，表示属性名，右边是一个对象。

```js
var obj={p:1};
'p' in obj //true
'toString' in obj //true
```

`in`运算符的一个问题是，它不能识别哪些属性是对象自身的，哪些属性是继承的。就像上面代码中，对象`obj`本身并没有`toString`属性，但是`in`运算符会返回`true`，因为这个属性是继承的。

这时，可以使用对象的`hasOwnProperty`方法判断一下，是否为对象自身的属性。

```js
var obj={};
if('toSting' in obj){
	console.log(obj.hasOwnProperty('toString'))//false
}
```

## 5.属性的遍历：for...in循环

`for...in`循环用来遍历一个对象的全部属性。

```js
var obj={a:1,b:2,c:3};

for(var i in obj){
	console.log('键名:',i);
	console.log('键值:',obj[i]);
}
// 键名： a
// 键值： 1
// 键名： b
// 键值： 2
// 键名： c
// 键值： 3
```

`for...in`循环有两个使用注意点。

- 它遍历的是对象所有可遍历（enumerable）的属性，会跳过不可遍历的属性。
- 它不仅遍历对象自身的属性，还遍历继承的属性。

举例来说，对象都继承了`toString`属性，但是`for...in`循环不会遍历到这个属性。

```
var obj={};

//toString 属性是存在的
obj.toString //toString() { [native code] }

for(var p in obj){
	console.log();
}//没有任何的输出
```

上面代码中，对象`obj`继承了`toString`属性，该属性不会被`for...in`循环遍历到，因为它默认是“不可遍历”的。关于对象属性的可遍历性，参见《标准库》章节中 Object 一章的介绍。

如果继承的属性是可遍历的，那么就会被`for...in`循环遍历到。但是，一般情况下，都是只想遍历对象自身的属性，所以使用`for...in`的时候，应该结合使用`hasOwnProperty`方法，在循环内部判断一下，某个属性是否为对象自身的属性。

```js
var person={name:'老张'};

for(var key in person){
	if(person.hasOwnproperty(key)){
		console.log(key);
	}
}
//name
```

## 6.with语句

`with`语句的格式如下：

```js
with(对象){
	语句;
}
```

它的作用是操作同一个对象的多个属性时，提供一些书写的方便。

```js
//例一
var obj={
    p1:1,
    p2:2,
};
with(obj){
    p1=4;
    p2=5;
}
//等同于
obj.p1=4;
obj.p2=5;

//例二
with(document.links[0]){
    console.log(href);
    console.log(title);
    console.log(style);
}
//等同于
console.log(document.links[0].href);
console.log(document.links[0].title);
console.log(document.links[0].style);
```

注意，如果`with`区块内部有变量的赋值操作，必须是当前对象已经存在的属性，否则会创造一个当前作用域的全局变量。

```js
var obj={};
with(obj){
	p1=4;
	p2=5;
}

obj.p1;//undefined
p1//4
```

上面代码中，对象`obj`并没有`p1`的属性，对`p1`赋值等于创造一个全局变量`p1`。正确的写法应该是，先定义对象`obj`的属性`p1`，然后在`with`区块内操作它。

这是因为`with`区块没有改变作用域，它的内部依然是当前作用域。这造成了`with`语句的一个很大的弊病，就是绑定对象不明确。

```js
with (obj){
	console.log(x);
}
```

单纯从上面的代码块，根本无法判断`x`到底是全局变量，还是对象`obj`的一个属性。这非常不利于代码的除错和模块化，编译器也无法对这段代码进行优化，职能留到运行时判断，这就拖慢了运行速度。因此，建议不要使用`with`语句，可以考虑用一个临时变量代替`with`。

```js
with(obj1.obj2.obj3){
	console.log(p1+p2);
}

//可以写成
var temp=obj1.obj2.obj3;
console.log(temp.p1+temp.p2);
```





## this的使用及指向

1. 函数(仅限于普通函数)创建时产生一个this

   ```js
   function box(){alert(this)}  指向window
   ```

2. (谁调用指向谁)当有事件绑定，并执行了事件处理程序时，谁绑定的事件，事件处理程序中的this指向谁

   ```js
   btn.onclick=function(){alert(this)}  绑定了事件，this事件的绑定者
   ```

3. 回调函数中的this指向window

   ```js
   setTimeout(function(){alert(this)})任何地方使用定时器，里面的this都指向window
   ```

4. 匿名函数可以使用bind()改变this的指向call()和apply()可以改变函数中的this指向

   ```js
   setTimeout(funciton(){alert(this)}.bind(btn))  使用bind()方法可以改变匿名函数this指向
   ```
   
5. 面向对象下的this

   ```js
   使用new关键字创建一个实例对象，构造函数中的this指向了该实例对象，同时实例对象的this指向构造函数的原型对象
   function Box(name){
       this.name=name;
   }
   Box.prototype.fun=function({this});
   new Box("tom").run();//this指向Box.prototype
   ```


## 继承

必须要调用，才可以使用，单单的赋值是没有办法使用的

继承跟父类没有任何影响	继承的只有属性和方法与值无关

**用完newMethod需要删除，防止下面的this指向newMethod**

```js
function classA(scolor){
    this.color=scolor;
    this.sayColor=function(){
        alert(this.color);
    }
}
function classB(scolor,sname){
    this.newMethod=classA;/将classA赋给classB中的一个属性newMethod
    this.newMethod(scolor);/调用——其实就是在调用classA
    delete this.newMethod;/用完newMethod需要删除，防止下面的this指向newMethod
    this.name=sname;
    this.sayName=function(){
        alert(this.name);
    }
}
function classC(scolor,sname,sage){
    this.newMethod=classB;
    this.newMethod(scolor,sname);
	this.age=sage;
    this.sayAge=function(){
        alert(this.age);
    }
}
var objA=new classA("green");
var objB=new classB("red","Lily");
var objC=new classB("blue","Tom",20);
console.log(objB);
console.log(objA);
objC.sayColor();/classC中没有sayColor classB中也没有sayColor classB从classA中继承而来的sayColor这个方法，继承的只有属性与方法，不包括值！！！
```

## 使用方法继承

将改变this的指向，继承给谁指向的就是谁

call apply bind()只能继承构造函数里面的属性和方法

使用构造函数继承的特点:直接把父类中的属性和方法集成到自己的构造函数中,在这个继承过程中使用call、bind()、apply

call和apply的用法是一样的，区别在于参数上边，**call的参数使用的是字符串来继承的，apply使用的是数组来继承的**

**继承过来之后自动调用,会调用.call之前的函数**不管几个call找的都是最后一个call之前的

1. call

   语法结构(对象，参数1，参数2，.......)；

   用法：构造函数.call/apply(对象,参数)；

   ```js
   function Animal(){
       this.name="Animal";
       this.sayName=function(){
           alert(this.name);
       }
   }
   function Cat(){
       this.color="yellow";
   }
   var animal=new Animal();
   var cat=new Cat();
   Animal.call(Cat,"");/使用字符串来写  继承的是Animal的属性和方法给cat
   //继承谁.call(谁继承,"参数","参数")
   cat.sayName();
   //继承过来后cat使用一次sayName这个方法
   ```
   
2. apply

   语法结构()

   有参数的话使用数组的方式来传

   ```js
   Animal.apply(cat,["red","lily"]); 
   ```

3. bind

   有参数的话用字符串来传

   与call的区别就是多调用一次

   ```js
   Animal.bind(cat,"")();/*不写引号就是全部都继承*/
   ```


## 原型链

prototype:是一个原型对象，可以存在与任何的构造函数中，之前的内置对象，在创建的时候都是用的new进行实例化的，换句话来说这些内置对象也是一个一个的构造函数

```js
String();
如果想要扩展String这个构造函数的属性和方法的话，那么我们就需要把这些属性和方法绑定在string这个构造函数的原型对象上。
String.prototype.属性名/方法名=值
如果在值中调用this的情况下，那么这个this执行的是new String("tom").run()这个this指向的是String.prototype
```

```js
__proto__:引用属性，隐形属性，当使用prototype找不到构造函数的情况下会使用__proto__这个隐形属性进行查找，在查找的过程中会一级一级的往上找，直到找到的object是null为止。再找的过程中会形成一个链式操作，这个链式操作就称之为原型链。
var str="123";
console.log(str.__proto__);
console.log(str.prototype);
通过prototype找到父类然后调用这个方法——如果prototype不指向这个属性才会再通过__proto__找

找的过程一层一层的向上查找就会形成一个链式结构，我们称为原型链——————直到null为止
```

## 原型链继承

```js
function Person(name){
    this.name=name;
};
Person.prototype.getName=function(){
    return this.name;
};
function test(){
    test.prototype.sex="man";
    test.prototype.getSex=function(){
        alert(this.sex);
    }
}
test.prototype=new Person("lily");//可以获取到Person与Person.prototype上的值
var a=new test();
a.getSex();
a.getName();
```

因为对象本身有prototype这个属性和__ proto__这个隐形属性，如果想要实现原型链的话，通过的是这两个属性实现的，原型链是一种链式操作，一层一层向上找，直到到null为止

## 构造函数继承

```js
function Person (name) {	//父类
    this.name = name;
    this.friends = ['小李','小红'];
    this.getName = function () {
        return this.name;
    }
};
function Parent (age) {		//子类
    Person.call(this,'老明');	//这一句是核心关键
    //这样就会在新parent对象上执行person构造函数中定义的所有对象初始化代码，
    //结果parent的每个实例都会具有自己的friends属性的副本
    this.age = age;
};
var result = new Parent(23);
console.log(result.name);	//老明
console.log(result.friends);	//['小李','小红']
console.log(result.getName());	//老明
console.log(result.age);	//23
console.log(result.getSex());	//这个会报错，调用不了父类原型上面扩展的方法
```

## 组合继承

call apply bind只能继承父类构造函数里面的属性和方法，在父类原型对象上绑定的属性和方法是无法继承的。

Strting->如果想要扩展string这个构造函数中的属性和方法的情况下，那么这些属性和方法就必须要绑定在string构造函数的原型对象上，那么这些属性和方法，我们通过call是继承不了的，所以我们需要通过原型链继承。

prototype只能继承父类构造函数原型对象上面的属性和方法，不能继承父类构造函数中的属性和方法。

如果我们使用的是原型链来进行继承的，那么原型链上面的this代表的就是父类.prototype

```js
function Person(name){
    this.name=name;
    this.friends=["小李","小红"];
};
Person.prototype.getName=function(){
    return this.name;
};
function Parent(age){
    Person.call(this,"老明");
    this.age=age;
};
Parent.prototype=new Person("老明");
var result=new Parent(24);
console.log(result.name);
console.log(result.getName());
result.friends.push("小智");
console.log(result.friends);
console.log(result.age);
var result1=new Parent(25);
//通过借用函数都有自己的属性，通过原型享用公共的方法 console.log(result.name);
console.log(result1.friends);//["小李","小红"]
```

组合继承和寄生组合继承的区别：

* 组合继承的话是直接使用call和prototype来继承到子类中
* 寄生组合继承：通过call先把父类的构造函数中的属性和方法继承过来，然后在继承父类原型对象上面的属性和方法的时候，通过一个中间类进行继承

## 寄生组合继承(中间类继承)

在这个过程当中，person依然是父类，parent依然是子类，使用中间类的好处是，父类不用反复调用，只需要调用一次父类即可，如果不使用中间类的话， 子类只要被实例化那么父类就会被调用，原型链不会变

缺点：多写代码

```js
function Person(name){ //父类
    this.name=name;
    this.friends=["小李","小红"];
}
Person.prototype.getName=function(){  //父类原型对象
    return this.name;
};
function Parent(age){  //子类
    Person.call(this,"老明");
    this.age=age;
}
(function (){
    var Super=function(){};//创建一个没有实例化的类中  中间类
    Super.prototype=Person.prototype;  //直接把父类原型对象上面的属性和方法给中间类的原型对象了
    Parent.prototype=new Super();  //将中间类实例作为子类的原型
})();//相当于把父类给了Super然后再实例化Super[其实实例化super就是在实例化Person]最后把他赋给子类就完成了继承
var result=new Parent(23);
console.log(result.name);
console.log(result.friends);
console.log(result.getName());
console.log(result.age);
```

* 继承方法：

  属性继承

  call、apply、bind()

  原型链继承

  构造函数继承

  组合继承

  寄生组合继承

## 面向对象的选项卡的封装

面向过程的封装：就直接写一个函数，通过传值的方式调用这个函数，找对象的时候直接找，直接操作

面向对象的封装：需要实例化一个对象，在实例化的这个对象中传值，找对象的时候是把对象作为构造函数的属性来操作的，如果需要操作这个对象的话就直接操作的是构造函数的属性，如果要绑定事件那么必须要有处理函数，这个处理函数是构造函数的方法，这个时候在处理函数中的this由构造函数变成了被绑定的属性了，这个处理函数是构造函数里面的方法，那么我们需要把this的指向重新定义，这也就是为什么有_this=this的原因

```js
window.onload=function(){
        new switchButton("div1","input","div");//实例化
    }
    function switchButton(id,In,di){
        var _this=this;//把this的指向重新定义 this指向switchButton
        var oDiv=document.getElementById(id);
        this.aBtn=oDiv.getElementsByTagName(In);
        this.aDiv=oDiv.getElementsByTagName(di);
        for(var i=0;i<this.aBtn.length;i++){
            this.aBtn[i].index=i;
            this.aBtn[i].onclick=function(){
                _this.fnClick(this);//_this指向aBtn[i]，指向不同所以才需要去声明
            }
        }
    }
    switchButton.prototype.fnClick=function(oBtn){//绑定在函数或函数原型上都可以
        for(var i=0;i<this.aBtn.length;i++){
            this.aBtn[i].className="";
            this.aDiv[i].style.display="none"
        }
        oBtn.className="active";
        this.aDiv[oBtn.index].style.display="block";
    }
```

## 深拷贝和浅拷贝

浅拷贝：当改变拷贝的对象里面的引用类型时，源对象也会改变。

深拷贝：互相不影响。

变就是深拷贝，不变就是浅拷贝

变量不存在深浅拷贝，只有数组和对象存在。

* 浅拷贝只在根属性上在堆内存中创建了一个新的的对象，复制了基本类型的值，但是复杂数据类型也就是对象则是拷贝相同的地址。
* 而深拷贝则是将一个对象从内存中完整的拷贝一份出来，从堆内存中开辟一个新的区域存放新对象，且修改新对象不会影响原对象。

```js
浅拷贝
var a=[0,1,2,3,4];
b=a;
console.log(b===a);
a[0]=8;
console.log(a,b);//指向的地址是一个
```

```js
深拷贝
function deepClone(obj){//是实现对象深拷贝的方法，参数obj是需要拷贝的源对象，用完这个方法之后需要返回一个新的对象，也就是使用深拷贝，拷贝出来的对象，它会指向一个新的内存空间。
    var objClone=Array.isArray(obj)?[]:{};//这个是创建出来的新对象，如果源对象是数组那就是空数组，是对象就是空对象
    if(obj!=null&&typeof obj==="object"){	//obj就是为了判断是否是空，typeof就是为了判断是否是对象，同时满足
        //判断obj子元素是否为对象，如果是，递归复制
        for(key in obj){//为了之后的复制做准备，因为不遍历没办法复制
            if(obj.hasOwnProperty(key)){//为了判断子元素是否为对象
                 if(obj[key]&&typeof obj[key]==="object"){
            		objClone[key]=deepClone(obj[key]);//直接使用递归函数进行调用即可
        		}else{
            		objClone[key]=obj[key];//如果不是，简单复制
        		}
            }
        }
        return objClone;
    }
}
let a=[1,2,3,4],
    b=deepClone(a);
a[0]=2;
console.log(a,b);
//互不影响
```

```js
//获取url转换成对象
function parseQuery(url){
 	var str=url.split("?")[1];
    var items=str.split("&");
    var arr,Json={};
    for(var i=0;i<items.length;i++){
        arr=item[i].split("=");
        Json[arr[0]]=arr[1];
    }
    return Json;
}
var obj=parseQueryString(URL);
console.log(obj);
```

##  防抖和节流

在进行窗口的resize、scroll，输入框内容校验等操作时，如果事件处理函数调用的频率无限制，会加重浏览器的负担，导致用户体验非常糟糕。此时我们可以采用debounce(防抖)和trottle(节流)的方式来减少调用频率，同时又不影响实际效果。

### 防抖

函数防抖：当持续触发时间时，**一定时间段内没有再触发事件**

原理：利用的是延迟器，让它在执行事件处理函数的时候，不立即执行，让它有一个延迟时间，如果在这个延迟时间里不再调用的话，那么到延迟时间的话就执行。如果在延迟时间里，再次调用的话，就清空上一次的调用，在本次执行的基础上进行延迟。

```js
//防抖
function debounce(fn,wait){
    var timeout=null;
    return function(){
        if(timeout!==null){
            clearTimeout(timeout);
        }
        timeout=setTimeout(fn,wait);
    }
}
//处理函数
function handle(){
    console.log(Math.random());
}
//滚动事件
window.addEventListener("scroll",debounce(handle,1000));
```

### 节流

函数节流：当持续触发时间时，保证**一定时间内只调用一次事件处理函数**。

两种：时间戳和定时器

用于：连续登录，如何阻止：节流

```js
时间戳
var throttle=function(func,delay){
    var prev=Date.now();//第一次执行的时候的时间,此次不会触发时间戳
    return function(){
        var context=this;//this指向window
        var args=arguments;//实参对象
        var now=Date.now();//再一次执行的时间
        if(now-prev>=delay){//当前时间减去上次触发时间如果大于等于延迟的时间才可以继续执行
            func.apply(context,args);//也可以写func()  ["hello",args]
            prev=Date.now();//触发时间，作为起始时间
        }
    }
}
function handle(){
    console.log(Math.random());
}
window.addEventListener("scroll",throttle(handle,1000));//谁触发this就是谁
```

```js
定时器
var throttle = function(func, delay) {            
    var timer = null;            
    return function() {                
        var context = this;               
        var args = arguments;                
        if (!timer) {                    
            timer = setTimeout(function() {                        
                func.apply(context, args);                        
                timer = null;                    
            }, delay);                
        }            
    }        
}        
function handle() {            
    console.log(Math.random());        
}        
window.addEventListener("scroll", throttle(handle, 1000));
```

# AJAX

对于网站来说最重要的两个东西一个是**网页**-->界面，一个是**数据**-->商品、店家

* 数据是由后台拿出来放到界面-->之前
* 数据由后台写完，前端放在界面中-->现在
* **上面的过程称为是：前后端的数据交互**

实现前后端数据交互的方法有很多：较为简单的是AJAX

## http协议

称为无状态协议，超文本传输协议

* 一个完整的http
  1. 首先是浏览器向服务器发送请求信息---拨号
  2. 然后服务器确定和浏览器请求之间的连接---接听
  3. 其次浏览器向服务器发送数据---说的事情
  4. 服务器端返回数据给浏览器，关闭连接---事情的内容，挂电话

## URL包含哪些内容

协议名：//域名/IP地址：端口号/文件名/文件路径

## AJAX

发送请求--必须要等到请求响应的情况下才会显示在页面中，并且如果想要再次发送请求的话必须等上一个请求完成，第二个请求才能发送。

必须完成一个之后才能进行第二个的请求和响应--同步

**AJAX是异步的js和xml**

## 异步

* js是一个单线程的，请求发送响应之后才能再次进行发送和请求的响应--同步
* **在整个的进程当中，可以有多个单线程，这些单线程是彼此不受干扰的**，例如：我们可以同时验证用户名和密码，用户名是一个线程，密码是一个线程，**这些线程是彼此不受任何干扰的，何时请求何时就可以进行响应。**

区别：同步必须等到请求响应之后才能再次发送请求，异步不需要等待。

js+css+dom+XMLHttpRequest

## AJAX在浏览器中是如何解析的

浏览器的架构：用户界面，浏览器引擎，浏览器内核，UI后端，数据存储，js解析器，网络

* **ajax可以直接通过浏览器进行解析---浏览器引擎的一部分（ajax引擎）**
* **ajax引擎--XMLHttpRequest对象**

## AJAX的工作原理(面试题)

1. 需要先创建一个AJAX对象——在js中创建由ajax引擎解析
2. 浏览器向服务器发送AJAX请求，过程中需要使用AJAX引擎进行解析，服务器接收到的是AJAX引擎解析之后的请求内容
3. 服务器响应请求发送给AJAX引擎，AJAX引擎解析响应，发送给浏览器的AJAX响应内容。

## AJAX的优势：异步

使用ajax的原因就是ajax可以实现异步操作

## AJAX对象的用法

1. 创建AJAX对象---XMLHttpRequest创建

   **有兼容性问题：IE-->ActiveXObject**

2. 设置要发送的数据--用户名密码给后台

3. 设置提交的方式--get/post，提交的路径

   **使用open(“get/post”【必须写其中一个】，url(路径)【是一个完整的路径，协议/域名/IP/端口/文件名】，true异步/false同步);**    **默认就是true**

   **url是后台提供给我们的一个接口路径，必须要是一个完整的路径：协议名，域名，端口，文件都需要加上，不能是一个本地的，必须是服务器上面的一个文件路径**

4. 设置头部信息--提交的时候用的是表单还是其他的方式进行提交

   方法：setRequestHeader("label","value");必须要放在open之后

   label：content-type:类型

   value：值：application/x-www-form-urlencoded

5. 处理相应的信息（函数）

   事件中，onreadystatechange：当数据返回的时候会调用这个事件，处理数据同样放在这个方法中

   **readyState属性（响应完成）**：存的是XMLHttpRquest对象的**状态**信息，从0到4的变化

   ​	0：请求未初始化（没有调用open方法）

   ​	1：服务器连接建立，但没有发送（调用了open()，没有调用send()）

   ​	2：请求已接收，开始处理请求

   ​	3：请求处理中，处理了一部分数据，响应还没有生成

   ​	4：请求响应完成

   **status属性（响应是否接收）**：

   以下为http状态码

   ​	200：“OK”成功接收

   ​	404：未找到页面

   ​	500：服务器端错误

6. 发送数据

   方法：send(要发送的数据)

## 返回值（返回的数据）

* responseText：字符串格式（包括Json格式的）【常用】
* responseXML：XML格式的（是一段代码）
* 拿例题来说我需要接收的是test.js文件中的内容，var obj={}，--responseText来进行接收的

**JSON:是一种轻量级的数据交换格式**

**属性和值必须都加上引号**

* eval()----eval("("+需要转换的对象+")");
* JSON.parse(需要转换的对象)

例子：

```js
//1.创建ajax对象，兼容性写法
var xmlhttp;
if(window.XMLHttpRequest){
    xmlhttp=new XMLHttpRequest();//正常创建ajax对象的方法
}else{
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");//字符串作为参数，ie6中创建ajax对象的方法
}

//2.设置要发送的数据，以下为模拟，正常情况下，这个数据是后台要告诉你的数据
var data="username=admin&pwd=admin";
//后台不要数据可以不提交，但是传过去的数据不需要我们操作

//3.设置提交的方式--url是后台提供给我们的一个接口路径--前面是站点后面是路径,直接从url这个文件中提取数据，因为目前提交的是本地的Js文件，不能使用post只能使用get
xmlhttp.open(“get”,"http://127.0.0.1:5500/js/test.js",true);

//4.设置头部信息--固定
xmlhttp.setRequestHeader("content-type","application/x-www-form-urlencoded")

//5.响应的处理
xmlhttp.onreadystatechange=function(){
    //这里做的操作是数据返回之后的操作但是在数据返回之前需要确定的是，和服务器连接成功，并且可以返回数据
   if(xmlhttp.readyState==4&&xmlhttp.status==200){
       console.log("数据获取完成");//为了验证，数据请求n'm完成，接收完成
       var res=xmlhttp.responseText;
       var resa=res.split("=");
       var obj=JSON.parse(resa[1]);
       console.log(obj.age);
       console.log(obj);
       for(var key in obj){//遍历对象输出
            var d=document.createElement("div");
            d.innerHTML=key+":"+obj[key];
            document.getElementsByTagName("body")[0].appendChild(d);
        }
    }
}

//6.发送数据,第二步中data
xmlhttp.send(data);//没有数据发送给后台的值就是null，写法就是xmlhttp.send()
```

* js文件--js文件中有一个对象

* 多个对象的话，一般我们使用的是数组来表示的

* 正常情况下，从后台提取的数据是不需要进行截取的，所以郑重情况下我们使用的是Json文件来进行获得的

* ```js
  [{
      "name":"why",
      "age":18
  },{
      "name":"zp",
      "age":18
  },{
      "name":"cxs",
      "age":18
  }]
  ```

1.对用户名进行验证，如果数据库中存在的话直接显示，否则不可用

* 思路：

  把所有的Json文件中的Name全部获取出来然后逐一和input值进行比对，如果有一样的情况下，显示：占用，否则：可用。

  2.json文件中的数据通过ajax进行获取

  3.需要在ajax中添加Input的事件

  4.用户名一旦存在， 就不能再进行循环比较了，没有意义 使用return false跳出

```js
xmlhttp.onreadystatechange=function(){
    if(xmlhttp.readyState==4&&xmlhttp.status==200){
        var res=JSON.parse(xmlhttp.responseText);
        use.onblur=function(){
            for(var i in res){
                if(res[i].name==use.value){
                    usa.innerHTML="用户名存在";
                    usa.className="error";
                    return false;
                }else{
                    usa.innerHTML="用户名可用";
                    usa.className="success";
                }
            }
        }
    }
}
```

2.用ajax验证用户名和密码：原理必须要在用户名存在的情况瞎才能进行密码的验证。

* 第一步：先验证用户名
* 第二步：再验证用户名存在的话验证密码

```js
user.onblur=function(){
	for(var i in perArr){
		if(user.value==perArr[i].name){
			usa.innerHTML="用户名已存在";
			document.getElementById("login").disabled=true;
			pwd.onblur=function(){
				if(pwd.value==perArr[i].pwd){
					document.getElementById("sub").disabled=false;
				}
			}
			return false;
		}else{
			usa.innerHTML="该用户需要注册";
		}
	}
}
```



## jQuery中的ajax

是把js中的ajax封装到了**$.ajax()**这个插件里面--方便，只需要设置参数即可。

* 参数

  url：需要提交到的页面是谁--open方法中的第二个参数

  data Type：服务器返回给我们的数据类型：xml、html、json、text-->object(如果没有会自动识别)

  type：设置提交方式：get/post，默认是明文get

  data：**向后台提交的数据，使用的是json格式的对象**

  async：同步false/异步true，默认异步true

  success：响应成功使用的回调函数-->function(){}

  ​	**正确的时候返回是请求文件中的数据**
  
  error：响应失败的回调函数-->function(){}
  
  ​	**错误的时候返回一个ajax对象**

```js
 $(document).ready(function(){
     $.ajax({
         url:"http://127.0.0.1:5500/js/2.json",
         type:"get",
         dataType:"json",
         data:{"username":"admin","pwd":"admin"}//传给后台的数据
     	 success:function(res){//res相当于js中的responseText
         $.map(res.function(value,index){//value-->数组中的对象
             $.each(value,function(key,value){//value-->数组中对象的属性值
                 $("body").append("<p>"+value+"</p>");
                 console.log("请求成功");//console.log(data),data返回的是获取出来的数据
             })
           })
     	},
         error:function(){//res-->返回一个ajax对象
             console.log("请求失败");
         }
     })
 })
```

* 响应成功之后，后台会传给前端数据，提取这些返回的数据。不管成功还是失败都会有回调函数，返回的数据就用回调函数的参数进行接收
* 在绑定事件的时候，直接绑定只能给页面中原有的元素进行绑定，新加的元素是不能进行绑定的，想要给新添加的元素添加事件需要使用live();

## jquery中的ajax，get/post

把Jquery中的ajax简写了而已

get或post请求方式是由后台设置的，数据同样也是由后台设置的，前端需要做的是通过请求把数据获取出来，当前的本地模拟只能用get,不能用post

**dataType:json,script,xml,html：这些文件里面的内容都不是我们写的，都是后台写的，所以我们只需要用**

<table>
	<tr>
		<th>请求文件类型</th>
		<th>dataType</th>
	</tr>
	<tr>
		<td>js</td>
		<td>script/text</td>
	</tr>
	<tr>
		<td>json</td>
		<td>json</td>
	</tr>
	<tr>
		<td>xml</td>
		<td>xml</td>
	</tr>
</table>

```js
$.ajax({
    url:"http://127.0.0.1:5500/js/2.xml",//test.js
    dataType:"xml",//script  text
    success:function(res){
        console.log(res);
    }
})
```

* $.get()--->type:get

  $.get(url，data，function(){})

  url：请求的路径

  data：传到后台的数据

  fun：请求成功返回的内容,也是在参数中继续接收

  ```js
  $.get("http://127.0.0.1:5500/js/2.json",{"name":"why","age":"18"},function(res){
      console.log(res);
  })
  ```

* $.post()-->type:post

  ```js
  $.post("http://127.0.0.1:5500/js/2.json",{"name":"why","age":"18"},function(res){
      console.log(res);
  })
  ```


## 跨域传值

ajax属于前后端交互的方式

* 前后端交互有两种形式

  1.在同一个域名，协议，端口---同源传值

  2.任何一个不一样都是---跨域传值

* **Question:什么是同源策略：**

  协议名，域名，端口号都相等的情况下就是同源，任何一个不相等就是跨域。

## 跨域传值的方式

1. location.search
2. jquery中的ajax
3. jsonp
4. postmessage
5. websocket
6. window+iframe

* **Question:js中的ajax能否进行跨域呢？**

  不能：XMLHttpRequest这个对象进行创建的，这个对象是受同源策略的影响，不能进行跨域，换句话来说原生的ajax就不能进行跨域

### 1.location.search跨域

跟ajax没有关系

decodeURI转换为中文 

* 对象赋值和获取的时候有两种方式，一种是对象.属性，对象[属性]
* 直接在a【链接】中写的内容和表单提交的内容是一样的。

```html
<a href="2020-3-6-zy1-b.html?username=admin&pwd=123456&sex=男&hobby=篮球">点击跳转</a><!--链接-->
    <form action="2020-3-6-zy1-b.html">    <!--表单-->
        <input type="text" name="name">
        <input type="password" name="pwd">
        <input type="submit">
    </form>
```

```js
function GetRequest(){
   var url=location.search;//使用loaction.search获取地址栏问号后面的内容
   var theRequest= new Object();//创建对象
   var str=url.substr(1);//去掉?
   var strNew=str.split("&");//将字符串按&分开      username=name   pwd=123456
   for(var i=0;i<strNew.length;i++){
      theRequest[strNew[i].split("=")[0]]=decodeURI(strNew[i].split("=")[1]);//将值名作为属性 name=value的形式 [0]存的是属性 [1]存的是值
   }
        return theRequest;
}
var con=GetRequest();
console.log(con);
for(j in con){
        var d=document.createElement("div");
        d.innerHTML=j+":"+con[j];
        document.getElementsByTagName("body")[0].appendChild(d);
}
```

### 2.jquery中的ajax

* **Question:jquery中的ajax不是封装的js中的ajax吗？为什么Jquery可以，js不行**

  jquery是把js封装起来了，封装的同时还同时封装了代理服务器(是怎么封装服务器的,不需要我们知道)，代理服务器功能就提供了Jquery中的ajax跨域的功能，所以Jquery中的ajax可以跨域，Js不行

* **Question:前后端交互和跨域传值搞混**

  前后端交互:可以是同源的也可以是跨域的

  跨域传值:一定是跨域的

jquery中的跨域传值使用$.ajax()即可

```js
$(document).ready(function(){
            $.ajax({
                url:"http://www.qhdlink-student.top/student/newsa.php",
                type:"post",
                data:{"username":"why58","userpwd":"123456","userclass":"58","type":"3"},
                dataType:"json",
                success:function(res){
                    console.log(res);
                    $.each(res,function(index,value){
                        console.log(value.title_news);
                        console.log(value.time_news);
                   $("body").append("<li class='a'>"+value.title_news+"<br>"+value.time_news+"</li>")
                    })
                },
                error:function(){
                    console.log("请求失败");
                }
            })
        })
//获取完数据之后,因为不知道数据有多少,所以需要手动添加到页面中加上标记,给标记添加样式可以使用id,class直接在标记中写即可
```

$.getJSON,$.getScript---->只能是get提交,不能用post提交,

​	   json 			script

$.getJSON(url,data,function(){//响应成功执行的内容})

$.getScript(url,data,function(){//响应成功执行的内容})

这两个互不影响

### AJAX引入图片

```html
<img src="url">
```

* src的路径：路径必须完整，协议名：//域名/ip:端口号/文件名
       直接用html中的img进行图片的加载，需要改的是src中的路径



### 点菜原理

加减功能：

* 加：如果点击按钮让后边的数量span相应的+1
* 减：如果单机按钮让前面的span相应的-1，但是如果数量到0了，那么就不能再减了，所以需要判断，当大于0才能再减，否则按钮不可用。
* 总价格：不管增加哪个菜品，相应的价格始终会+当前菜品的价格，当减少这个菜品的时候，总价格相应的也会减少，找的是当前div中存有价格的标签里面的html的值。



根据一个接口调取另一个接口，甚至更多的接口，在调取的过程中，进行传值，调取更深层的接口是由前一个接口传值得来当前接口的内容，两个页面中都需要使用ajax接口的调用

### 3.jsonp-->只能使用get提交传值

* **Question:jsonp和json有什么关系？**

  没关系，用jsonp这种跨域传值的方式获取的是**json格式**的数据。

* **Question:为什么有jsonp?**

  ajax因为XMLHttpRequest这个对象的关系，所以只能同源传值，不能跨域传值，就有了使用jsonp进行跨域的方式。

**jsonp的原理：**

src:特点是不管什么文件，或者哪个地方的文件都可以进行加载，换句话来说，src这个属性是不受跨域影响的。

所以在使用jsonp的时候就是用src传的值。因为一直使用jsonp的方式结合src进行数据的传输，服务器和客户端的数据传输，规定了一种非正式的传输协议：sonp-->src进行传值的过程中我们会需要接收数据，在传值的时候会传一个callback这样的参数，这个参数的值是一个函数(callback回调函数)，接收数据的时候通过callback回调函数来进行数据的接收的，接受完这些数据之后，那么我们就需要通过callback这个回调函数来操作这些数据

```js
url:ip? callback=test-->写test这个函数的目的，就是为了对后台的数据进行解析//前面的参数名必须叫callback后面可以随意
test这个回调函数-->callback回调函数
src进行传值，那么也就意味着只要有src这个属性的标记都可以作为传值的方式-->script
```

* **Question:说一下jsonp的原理**

  利用src这个属性进行传值，在传值的过程中使用的是sonp这个非正式传输协议，然后利用callback这个回调函数来传递和接收数据的，在传的过程当中用户会传递一个叫callback的参数，在这个参数中存的是一个回调函数给服务器，服务器通过callback参数把json格式的数据传送给客户端，客户端对json格式的数据使用这个回调函数进行解析

```html
<script type="text/javascript">
function jsonpCallback(res){
    console.log(res);
}
</script>
<script type="text/javascript" src="http://127.0.0.1:5500/js/2.json?callback=jsonpCallback">
</script>
```

```js
//js

jsonpCallback(["name":"why","age":"18"])
//可以传字符串
jsonpCallback("Hello world");
//也可以使用变量来替代
var obj=["name":"why","age":"18"];
jsonpCallback(obj);
```

```json
jsonpCallback([{"name":"why","class":"58","age":"18"}]);
```

jsonpCallback这个回调函数是用参数来接收的后台传过来的数据，那么后台会进行一些操作，后台调用这个jsonpCallback回调函数传给前端数据，传给前端的数据直接放在参数中

jsonpCallback-->作为的jsonp的回调函数来使用，那么一旦这个回调函数的名字发生改变了，会连同这个所有的回调函数都改变，换句话来说，这个回到函数的名字要跟后台的保持一直，后台直接给你接口就直接使用即可。

**在jsonp中不需要像ajax一样设置dataType,传的参数是什么那么我们接收到的就是什么。**

* html中标记的创建可以有两种形式

  1.直接写script

  2.使用js创建的script，DOM节点-->createElement，直接用src属性添加。

  ```html
  <script type="text/javascript">
          var s=document.createElement("script");
          s.src="http://127.0.0.1:5500/js/2.json?callback=test";
          document.getElementsByTagName("body")[0].appendChild(s);
          function test(res){
              console.log(res);
          }
  </script>
  ```


### jquery封装jsonp

jquery中的ajax在使用jsonp的时候依旧会使用和设置callback，同时也会需要一个回调函数来进行传值和接收值

dataType:设置的返回数据，json，ajax中同时也封装了jsonp，设置jsonp

* **dataType:jsonp-->设置ajax的请求方式是jsonp**
* **jsonp:callback-->设置callback参数**
* jsonpCallback:回调函数
* 单独使用jsonp的时候，我们需要自己写回调函数，而在ajax封装的jsonp中，他的返回值也是在success中得到，所以直接写success即可。

```js
在url中不需要写问号后面的东西，
url:"http://127.0.0.1:5500/js/1.js",
dataType:"jsonp",
jsonp:"callback",//设置callback参数
jsonpCallback:"test"//文件中的函数名   回调函数
success:function(res){
    console.log(res);
}
```

* 返回数据：后台写的是什么数据，前端就会返回什么数据，在jsonp中不需要进行数据类型的设置，**但是在ajax中需要使用dataType设置返回的数据类型**

### 4.postMessage

是H5中封装的XMLHttpRequest也就是跨文本消息传递

一般如果需要使用框架嵌套的时候，那么传值就会用iframe的方式进行传值

**区别**：之前的ajax或Jsop直接获取数据操作，postmessage是通过postmessage进行传值的，传值的时候直接把值放在postMessage中的data里面进行传值，所以postMessage多操作于页面和页面之间的传值。

* ajax和jsonp：给我们的是一个js文件或者是json文件或者是一个接口文件，我们是直接从这个接口文件中获取的值。

* postMessage：数据是存在于一个html中，我们再另外的一个html进行数据的接收：父页面-->子页面传值，就可以使用postMessage进行传值，它不仅可以父向子传，同时可以子向父传，传值可以是相互的。

iframe因为它也有src这个属性，所以也可以实现跨域传值

* postMessage(data,orign);

  data：操作的数据(设置数据需要注意的是最好是json格式，因为有一些浏览器不支持json格式，用字符串也可以)【传参的时候最好使用JSON.stringify()序列化 ：需要把他转换成字符串】

  orign：要提交的地址url

1. 在父页面中使用postMessage进行传值，传给子页面

   当父页面传值的时候子页面会触发一个事件：message，会把传过来得数据放在参数中进行接收，参数在接收的时候接收到的是一个postMessage对象，数据就存在于这个对象中。

   postmessage是一个方法，这个方法的对象就是接收数据的对象（子页面）

   子页面.postMessage()，子页面

2. postMessage得原理：

   * 在父页面中通过postMessage进行传值，传给子页面把postMessage中的值
   * 在子页面中会触发一个叫message得事件，接收到得数据放在得是事件对象得data属性中
   * 在传值得时候因为多数浏览器支持字符串的格式，所以我们需要使用JSON.stringify()进行转化

* **使用iframe进行postMessage传值**

```html
<div>我是子页面</div>
<script>
	window.addEventListener("message",function(res){//res-->message的事件对象
	console.log(res);
        console.log(res.data)//获取数据
	})
</script>
```

```html
<div>我是父页面</div>
<iframe src="right.html"></iframe>
<script>
	window.onload=function(){
        window.frames[0].postMessage(JSON.stringify({"name":"lily"}),"http://127.0.0.1:5500/js/right.html");
    }
</script>
```

* 子-->父：window.parent
* 在子页面中使用postMessage向父页面进行传值
* 在父页面中触发message事件进行数据的接收

细节：target：_blank、 _self、 _parent(父窗口)

```html
<div>我是子页面</div>
<script>
	window.addEventListener("message",function(res){//res-->message的事件对象
	console.log(res);
        console.log(res.data)//获取数据
//子向父传的
        window.parent.postMessage("我是子页面传过来得","http://127.0.0.1:5500/js/left.html")
	})
</script>
```

```html
<div>我是父页面</div>
<iframe src="right.html"></iframe>
<script>
	window.onload=function(){
        window.frames[0].postMessage(JSON.stringify({"name":"lily"}),"http://127.0.0.1:5500/js/right.html");
    }
//子向父传的
    window.addEventListener("message",function(res){
        console.log(res.data)
    })
</script>
```

* **使用window.open实现postMessage传值**

原理：

* 父-->子
  父页面：利用window.open重新打开一个新窗口的原理,使用postMessage(data,orign)方法向子页面传输数据，但需要注意的点是父页面需要一个异步的操作，因为如果设置为打开的同时传输即为同步，无法传输，所以设置一个延时器进行传输
  子页面：接收数据时触发事件message，res.data是数据的内容

* 子-->父：其实是与之相反的
  子页面：子页面利用一个属性window.opener即找到父页面,然后重复使用postMessage(data,orign)方法
  父页面：父页面接收的时候也会触发message事件，res.data是接收的内容
  这里需要注意的是不能直接打开子页面查看接收的数据，因为是有顺序的即：父向子传输，子接收到之后向父传输。

细节：

* 在使用window.open打开子页面的时候，如果使用window.opener向父页面传值，必须要先打开一遍子页面才行，因为向父页面传值是接收到父页面值之后才传的，所以需要先打开。

```html
<!--父页面-->
<script>
	var win=window.open("http://127.0.0.1/js/son.html");
    setTimeout(function(){
        win.postMessage("父页面传来的值","http://127.0.0.1/js/son.html");
    },5)
    
    window.addEventListener("message",function(res){
        console.log(res.data)
    })
</script>
```

```html
<!--子页面-->
<script>
	window.addEventListener("message",function(res){
     console.log(res.data);
        
     window.opener.postMessage("子页面传来的数据","http://127.0.0.1/js/father.html");
    })
</script>
```

### 5.window.name+iframe

* window.name:name的值在不同的页面加载后仍然可以存在，可以支持较长的name值（2M）

* url:受地址栏个数限制的，name不受影响【2M之内】

* **iframe作用：传值--->对于浏览器来说禁止跨域传值**

* window.name使用iframe切换页面时，window.name中的值是不变的

* 思路：

  三个页面：两个同源页面，一个跨域页面

  父页面中：获取跨域页面的值----里面嵌套了一个iframe

  子页面：媒介作用

  iframe中有两次变化：

  1. 跨域的页面：加载完成后传window.name的值，页面加载完成后把name值传给父页面同源的子页面
  2. 更改iframe中src的值，改成同源的子页面，这时window.name的值是不会发生变化的，这个值是由子页面传给父页面的

```html
<!--left页面-->
<iframe src="http://127.0.0.1:5500/js/score.html" id="iframe" onload="load()"></iframe>
<script>
	let y=true;
    function load(){//会执行两次，每一次都是由score页面触发的，第二次是由right页面出发的
        if(y){
            let iframe=document.getElementById("iframe");
            iframe.src="http://127.0.0.1:5500/js/right.html";
            y=false;
        }else{
            console.log(iframe.contentWindow.name);//找iframe上的window.name的值
        }
    }
</script>
```

```html
<!--score页面-->
<div>我是score.html</div>
<script>
	window.name="我是score页面传过来的值";
</script>
<!--right页面-->
空
```

**document.domain+iframe**：

* document.domain：只有在两个页面二级域名相同的情况下才能跨域，端口号也要一样

  a.cc.com	taobao.com

  b.cc.com	jd.com

* 原理：

  两个页面通过js强制设置document.domain为基础主域的目的是为了两个页面实现同源

  iframe只能在同源情况下进行传值

  用document.domain的原因就是为了强制让两个域名为主域，设置完主域之后就是同源了，换句话来说也就可以通过iframe进行传值了

  window.name--->iframe.contentWindow.name

  iframe.contentWindow.变量名

```html
<!--left页面-->
<iframe src="http://b.cc.com/right" onload="load()"></iframe><!--连接right.html这个页面-->
<script>
	//域名是a.cc.com/left.html
    document.domain="cc.com";
    function load(){
        let iframe=document.getElementById("iframe");
        console.log(iframe.contentWindow.a);//获取值
    }
</script>
```

```html
<!--right页面-->
<script>
	//域名是b.cc.com/right.html
    document.domain="cc.com";
    var a=10;
</script>
```

### 6.webSocket

浏览器提供给我们的一个API，可以提供**双向通信、全双工，且只能跨域不能同源**

服务器与浏览器在传输的时候需要进行三次握手，**而websocket中只需要一次握手即可进行数据的传输，同样也是通过TCP/IP协议进行数据的传输**

工作原理：浏览器向服务器发送websocket请求，发送完成链接建立，数据可以在服务器和浏览器之间进行双向传输

浏览器发送数据使用的是send方法，接收数据使用的是message事件进行接收的，接收和传输的是http请求

* 创建websocket对象：

  new进行创建-->new WebSocket(url，protocol);

  url:代表发送和接收数据的文件路径

  protocol:代表协议-->http 可以不写

* 特点：

  1.建立在tcp协议之上进行通信

  2.与Http有较好的兼容性

  3.数据轻，性能和效率高

  4.可以发送文本也可以是二进制数据

  5.没有跨域限制，客户端可以与任意服务器通信

  6.协议标识是ws，加密用wss，服务器网址就是url

* readyState属性

  0：为建立连接

  1：已经建立可以发送

  2：连接正在关闭

  3：已经关闭或链接无法打开

  * ajax中的readyState：是需要进行三次握手的，客户端发送请求，服务器进行响应，4的时候是成功的
  * websocket：只需要一次握手，客户端发送完请求直接连接成功，所以1的时候数据是可以传输的

* 事件：

  open：建立连接会触发

  message：客户端接收数据会触发

  error：通信错误时触发

  close：代表连接关闭时触发

* 方法：

  send()：发送数据

  close()：关闭连接

* 用法：

  1. 先创建一个websocker对象
  2. 创建完成之后进行事件的触发，先触发open，如果需要发送直接使用send发送
  3. 客户端接收数据的时候会触发：message事件，接收的数据放在事件对象的data属性中
  4. 当接收完之后如果不需要发送数据的话直接可以关闭
  5. 关闭完成之后触发的是close事件

```html
<script>
	var ws=new WebSocket("wss://echo.websocket.org");
    ws.open=function(){
        console.log("连接已建立");
        ws.send("发送数据");
    }
    ws.onmessage=function(e){
        var e=e||window.event;
        console.log(e.data);
        ws.close();
    }
    ws.onclose=function(){
        console.log("连接已关闭");
    }
</script>
```

```html
<script>
//封装websocket
function WebSocketTest(url){
    alert("您的浏览器支持WebSocket");//window.WebSocket两者是一样的
    //打开一个websocket
    var ws=new WebSocket(url)	//创建一个websocket对象
    ws.onopen=function(){	//连接
        //websocket已连接上，使用send()发送数据
        ws.send("发送数据");//触发的是数据发送方法
        alert("数据发送中...");
    };
    ws.onmessage=function(evt){//接收数据的事件
        var received_msg=evt.data;
        alert("数据已接收");
    };
    ws.onclose=function(){//关闭连接的时候触发的事件
        //关闭websocket
        alert("连接已关闭");
    };
    else{
        //浏览器不支持websocket
        alert("您的浏览器不支持websocket");
    }
}
</script>
<div id="sse">
    <a href="javascript:WebSocketTest('ws://localhost:8080')">运行WebSocket</a>
</div>
```

* websocket事件触发的顺序：

  没有错误时：open-->message-->close

  发生错误时：无论是哪个过程发生了错误都会执行error

### 7.cors

cors：跨域资源共享

是W3C规定的一个跨域资源共享的标准

作用：告诉服务器和浏览器是如何进行沟通的

原理：使用自定义的http请求让服务器和浏览器进行沟通，从而决定请求是成功还是失败。如果想要使用cors请求的话，服务器和浏览器必须同时支持才行（必须同时使用才行）

IE不能低于IE10

```
只要同时满足以下两大条件，就属于简单请求。

请求方法是以下三种方法之一: HEAD、GET、POST

HTTP的头信息不超出以下几种字段: Accept、 Accept-Language、 Content-Language、Last-Event-ID、 Content-Type

Content-Type:只限于三个值application/x-www-form-urlencoded、 multipart/form-data、text/plain
```

简单请求不需要浏览器做任何操作，是在服务器上完成的操作，不需要前端操作。

非简单请求：需要服务器和浏览器同时设置，换句话来说服务器需要设置浏览器允许访问的接口地址，除此之外服务器还需要设置请求头，以及请求类型

* 浏览器需要设置：

  Access-Control-Request-Method:请求方法

  Access-Control-Request-Headers:自定义得头部信息

* 浏览器设置cors：

  setRequestHeader:设置相应的头部信息

  setHeader():设置cors请求

  例如：

  response:请求对象

  * response.setHeader("Access-Control-Request-Method","post/get");请求方法

  * response.setHeader("Access-Control-Request-Headers","Orign,X-Request-With,Content-Type,Accept");头部信息

  * response.setHeader(“Access-Control-Allow-Origin”,"*"):是否允许跨域请求，星号代表允许任何跨域请求

    http://www.a.com:那么只允许从a域名发送的跨域请求

原生的ajax不支持跨域，那么我们在写的时候，还是和之前的ajax的写法一样，那么在open：是设置请求的路径，在使用cors请求的话直接把open中的url换成一个跨域url即可

* ajax.open("post","http://www.a.com/test.json",true)

```js
var xmlhttp=new XMLHttpRequest();
xmlhttp.open("get","http://www.a.com/test.js",true);
xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencode");
xmlhttp.onreadystatechange=function(){
    if(xmlhttp.readyState==4 && xmlhttp.status==200){
        console.log(xmlhttp.responseText);
    }
}
xmlhttp.send();
```

```
var http=require("http");
var server=http.createServe();
server.on("request",function(req,res){
	res.setHeader("Access-Control-Allow-Origin","*");
	//http://
	res.setHeader("Access-Control-Allow-Headers","Content-Type");
	res.setHeader("Access-Control-Allow-Methods","get");
	res.end("data");
})
```

## 浏览器的渲染过程

* 页面分为三层：

  html：结构层，css：表现层，js：样式层

* 浏览器先解析的是html结构层，结构层中的标记转换成DOM中的节点
* 加载html结构的同时，如果有link，会连同样式一起进行加载，对整个页面进行渲染，在渲染的过程中采取的是流式加载，从上往下，从左往右依次进行加载的。

  加载的Html和css的过程中，如果遇到js的话会立即终止对css和html的加载，直接加载js的内容，也就是为什么js放在body中找不到DOM的原因，因为DOM还没有加载。

  在整个的加载过程中，采取的是流体加载布局，但是也会出现一些特殊情况，例如：脱离文档流，就会影响上下文的布局，所以会有回流的现象出现。
* DOM：文档对象，层级--DOM树

  DOM的作用是会把整个页面划分成一个有层级关系的DOM树

* DOM的级别<font color=#f00>【面试题！！！】</font>

  DOM1级：允许获取和操作文档的任意部分

  DOM2级：鼠标和用户界面事件，以及对CSS的支持和遍历

  DOM3级：对文档存储、载入、验证的方法

### DOM事件级别

* DOM0级：规定了行内事件的绑定
* DOM2级：通过addEventListener来绑定事件
* DOM3级：新增的事件（例如移动端的一些事件）

### 新增事件

* onunload：退出页面相当于关闭页面，也就看不见这个事件的触发和显示内容。

* <font color=#f00>onbeforeunload</font>：即将离开当前页面（刷新或关闭）时触发。【有兼容性问题】

  ```js
  window.onbeforeunload=function(e){
      e.returnValue="你要离开页面吗";
  }
  //returnValue:属性，代表的是自定义信息
  ```

  谷歌/欧朋不支持，火狐和IE会根据浏览器自身的设置进行提示

* <font color=#f00>onpageshow</font>：用户浏览网页时触发

* <font color=#f00>onpagehide</font>：当窗口离开，隐藏

  ```js
  document.getElementsByTagName("body")[0].onpageshow=function(){
  	alert("页面被触发");
  }
  window.onpagehide=function(){
      alert("页面离开");
  }
  ```

* onafterprint：文档打印之后运行的脚本

* onbeforeprint：文档打印之前运行的脚本

  ```js
  window.onafterprint=function(){
  	console.log("页面打印完了");
  }
  window.onbeforeprint=function(){
      console.log("页面要打印了");
  }
  window.print=function(){
      window.print();
  }
  ```

* onerror：在错误发生时运行的脚本

  ```js
  document.getElementsByTagName("img")[0].onerror=function(){
  	alert("图片加载有误");
  }
  ```

* onhashchange：当#后面的内容改变时会触发。

  ```js
  function change(){
      location.hash="#aa";
  }
  document.getElementByTagName("body")[0].onhashchange=function(){
      alert("锚点发生了改变");
  }
  ```

  `获取#后面的：location.hash`

  `获取?后面的用:location.search`

* onmessage：在消息被触发时运行的脚本

  `在postMessage中使用message事件对数据进行接收`

* onoffline：当文档离线时运行的脚本

* ononline：当文本上线时运行的脚本

  ```js
  document.getElementsByTagName("body")[0].ononline=function(){
      alert("浏览器开始工作了");
  }
  document.getElementsByTagName("body")[0].onoffline=function(){
      alert("浏览器要离开了");
  }
  ```

  `兼容性：火狐支持，ie8-10支持`

* onpopstate：当窗口历史记录改变时运行的脚本

* onredo：当文档执行撤销（redo）时运行的脚本。

* onstorage：在web Storage区域更新后运行的脚本。

* onundo：在文档执行undo时运行的脚本

### 新增表单事件

* onformchange：在表单改变时运行

  ```js
  document.getElementById("myForm").onformchange=function(){
  	console.log("改变了")
  }
  ```

* onforminput：当表单获得用户输入时运行

* oninput：当元素获得用户输入时运行

* oninvalid：当元素无效时运行

  与h5中新增的invalid属性基本一样：在元素无效的时候触发

  required：不允许为空

  ```html
  <form action="#" id="myForm">
      <input type="text" id="username" required>
      <input type="submit">
  </form>
  ```

* ondrag：拖动标记触发

  ```js
  document.getElementById("p1").ondrag=function(){
  	alert("你拖动了这个P标记");
  }
  ```

* ondragstart：开始拖动的第一次触发

  ```js
  document.getElementById("p1").ondragstart=function(){
  	alert("你拖动了这个P标记");
  }
  ```

  如果想让元素可以进行拖动，必须要加上的属性：draggable="true";

* oncontextmenu：右击指定标记触发

### Touch事件--移动端

##### Touch列表属性

* identifier，一个数值，标识触摸会话中的那个手指的id
* 剩下的属性同事件对象的属性一致

touch的属性列表中所有的属性不存在任何兼容性问题

* touchstart：触摸开始触发
* touchmove：移动触发
* touchend：触摸结束触发

移动端的事件需要使用addEventListener来进行绑定，不需要考虑兼容性问题，移动端的浏览器都是最新的，都会支持事件监听的绑定方式

```js
document.getElementById("p1").addEventListener("touchstart",function(){
    alert("你触摸了这个div");
})
```

* 触摸列表对象全部都存在事件对象中进行使用

  <font color="#ff0">touches：代表所有手指的一个列表，是一个集合（数组），只要手在屏幕上就可以获取值。</font>

  ```js
  document.getElementById("p1").addEventListener("touchmove",function(e){
  	//e.touches[]
      var x=e.touches[0].clientX;
      var y=e.touches[0].clientY;
      this.innerHTML=x+","+y
  })
  ```

  <font color="#ff0">targetTouches:当前手指在DOM元素上面列表</font>

  ```js
  document.getElementById("p1").addEventListener("touchmove",function(e){
  	//e.touches[]
      var x=e.targetTouches[0].clientX;
      var y=e.targetTouches[0].clientY;
      this.innerHTML=x+","+y
  })
  ```

  changedTouches：当前事件的一个列表

## 移动端轮播图

* touchstart----clientX

* touchend-----clientX

  两个值相减，如果start-end：

  -显示上一张

  +显示下一张

### 手势事件

手势事件是由多个手指进行触发的，gesture

* gesturestart

* gesturemove

* gestureend

* 如果想要触发手势事件必须要先触发touch事件

* touchstart--gesturestart--gestureend--touchend

  ```js
  document.getElementById("d1").addEventListener("gesturestart",function(e){
      alert("gesturestart事件")
  })
  ```

gesture手势事件是把所有的手势事件进行具体化了，不管是触发的哪个手势都会执行gesture事件

touch.js中的事件，把gesture可以用到的手势都整理出来了，缩放，滑动，拖动，旋转，单击，双击，长按具体分解到每一个事件上了，所以再用的时候不兼容gesture事件的话，使用touch.js这个插件来完成。

### touch.js插件

**多个事件之间使用空格隔开**

### 下滑加载的原理

* touchstart-->clientX

* touchend-->clientY

  两者相减：+的话就加载下面的内容（可以是复制上面的，也可以是先添加createElement进行添加，每次都多+10来显示）

  ```js
  touch.on(document.getElementById("p1"),"rotate",function(){
      this.style.webkitTransform="rotate(30deg)";
  })
  ```

  ```js
  touch.on(document.getElementById("p1"),"pinchstart",function(){
      this.style.webkitTransform="scale(2,2)";
      alert("你缩放了这个div");
  })
  ```

  ```js
  touch.on(document.getElementById("p1"),"touchstart",function(e){
      e.startRotate();//获取的是初始化的角度，不获取的话就是从原来的0°进行旋转，获取的话会从当前的角度进行旋转
      e.preventDefault();//为了阻止浏览器默认缩放或滚动条滚动
  })
  touch.on(document.getElementById("p1"),"rotate",function(e){
      this.style.webkitTransform="rotate("+e.rotation+"deg)";
  })
  ```

  ```js
  //想让当前的p标记有动画效果
  document.getElementById("p1").style.webkitTransition="all 0.5s";
  //一般在使用touch.js的时候，尽量让浏览器的所有的默认动作都阻止掉，只要是手指触碰到当前的屏幕，那么就要阻止浏览器默认行为--touchstart事件
  touch.on(document.getElementById("p1"),"touchstart",function(e){
      e.preventDefault();
  })
  //接下来再使用touch.js中的其他手势事件进行相应的操作
  ```


## 本地存储和离线存储

* 存储

  首次登陆一个账号的时候，可以免登录，因为是将用户名和密码保存下来了

### 本地存储和离线存储、cookie

1.本地存储：

webStorage---H5新增API，对于主流浏览器来说都是可以兼容的

把信息存储到本地电脑上，客户端在进行存储的时候遵循“同源策略”，不同站点【网站】之间是无法进行存储的，相同站点下的不同文件之间可以进行调用

* webStorage好处：

  进行存储的时候是保存在本地的，不会在服务器上进行保存，也就是说它不会影响当前页面的性能，并且可以存储大量数据，存储比较高效和安全，服务器只让用户请求数据

  

* webStorage分为两种存储

  1. localStorage：永久存储--一直在

  2. sessionStorage：临时存储--浏览器关了就没了

#### localStorage

存值：localStorage.属性名=值

永久存储，会一直存储在本地，只要是同源的页面之间都可以进行数据的获取，同样也可以进行修改，同源页面之间多次给同一个属性进行赋值会被覆盖掉。

```js
//1.存数据--这种使用的多
localStorage.username="lily";
//获取数据
console.log(localStorage.username);
//换保存的数据，重新对username属性进行赋值即可
localStorage.username="Tom";
console.log(localStorage.username);
//里面是没有值了，但是他是一个空的字符串，实际上并没有username进行清空，只是让里面没有值了
localStorage.username="";

//2.存储值
localStorage.setItem("pwd","123456789")
//获取值
console.log(localStorage.getItem("pwd"));
//删除数据，删除指定一个用removeItem
localStorage.removeItem("pwd");
console.log(localStorage.pwd);
//全部清空
localStorage.clear();
console.log(localStorage.username);
```

#### sessionStorage

临时存储

同源页面之间可以进行数据的传递

和localStorage的区别：只能临时存储在浏览器中，只要浏览器关闭了，那么数据也就不存在了。

sessionStorage的用法和localStorage的用法完全一样，包括创建缓存，清空缓存

同时在sessionStorage和localStorage创建了username，两个之间是不会冲突的，因为对象就不一样

即使是同源页面之间，在一个页面中保存了sessionStorage的值，单独打开其他页面是获取不到这个值的，只有两个页面进行链接的话才能获取到值。

* 创建sessionStorage

  直接对属性进行赋值，或者setItem方法进行创建

* 获取

  通过属性获取，或者getItem方法进行获取

* 删除

  删除某一个缓存使用removeItem(属性)

* 全部清空：clear

```js
//创建
sessionStorage.setItem("pwd","123456");
//获取
sessionStorage.getItem("pwd")
//删除
sessionStorage.reoveItem("pwd");
//清空
sessionStorage.clear();
```

sessionStorage和localStorage区别：

存储的有效期和作用域不同

* sessionStorage:临时 	被限定在窗口中，无法共享
* localStorage:永久        不同页面也可以互相读取，设置覆盖修改

适用范围：

* localStorage-->PC
* sessionStorage-->移动端

#### cookie

试想客户端浏览器保存信息的一个文件，文件是以文本文档的方式进行保存的，生成是由服务器端生成的，发送给浏览器，浏览器以键值对【属性：值】的方式，保存在文本文档中（用户名和密码）。当下次再访问这个网站时，会把cookie中的数据发送给服务器进行比较， 比较成功登陆，比较不成功重新输入用户名和密码，同时保存到原来的cookie文件中（对原有的cookie文件中的内容进行更新/覆盖）

cookie是一个小文件，大概能存4kb

##### cookie的原理

是由服务器端创建的，创建完成之后发送给客户端，客户端本地会有一个文件进行cookie的保存，什么时候需要什么时候提取和比对

* **与webStorage的区别：**

  1.**存储空间的不同**

  webStorage提供的存储空间要比cookie大
  
  如果有子域的情况下，webStorage，每一个子域下都有自己的存储空间，而cookie没有
  
  2.**接口**
  
  webStorage提供了很多接口，操作方标：setItem,getItem等
  
  cookie只有自己封装的setCookie和getCookie等。
  
  3.**cookie的数据始终是在同源的http请求中携带的（不要cookie，那么在发送请求的时候也会一起发送）**
  
  webStorage不会跟着请求一起发送
  
  4.**有效期不同**
  
  localStorage：永久存储
  
  session：临时存储，浏览器关闭，数据销毁。
  
  cookie：过期时间之内有效
  
  5.**作用域不同**
  
  localStorage、cookie：所有的同源页面都可以共享
  
  sessionStorage：只能在同一个页面中进行共享

各浏览器cookie个数限制

* FF每个域名cookie限制为50
* Opera每个域名限制为30
* safari/webkit没有限制，但是很多的话会导致错误发生
* IE8每个域名：50，IE7每个50，IE每个20

cookie有两种用法

* 会话关闭cookie就删除
* cookie可以设置过期时间（永久）（例如：7天免登录，这个过期时间就是7天）

##### 判断浏览器是否支持cookie

```js
if(navigator.cookieEnabled){
    alert("支持cookie");
}else{
    alert("不支持cookie");
}
```

##### 创建cookie

* document.cookie创建

```js
//在cookie中创建的一个临时
document.cookie="username=123;expires=时间"
在cookie中创建的一个用户名，expires：设置的是过期时间，如果没有设置过期时间的话，呢么创建出来的cookie就是一个临时cookie
```

过期时间是一个毫秒数

##### 读取cookie

* document.cookie值

##### 删除cookie

将时间设置成过期时间，浏览器会自动进行删除

##### 修改cookie

与创建cookie用法一样，对cookie进行直接赋值

```js
if(navigator.cookieEnabled){
    document.cookie="username=123456;expires="dd+";path=/";
}else{
    alert("不支持cookie");
}
var obj=new Object();
console.log(document.cookie);
var arr=document.cookie.split("=");
console.log(arr[0]+","+arr[1]);
obj[arr[0]]=arr[1];
console.log(obj.username);
```

## 离线存储

没有网络的情况下仍可以进行访问，在操作的时候把需要的文件：css、js、图片等文件保存到本地，那么在没有网访问的时候直接从保存的本地文件中进行提取，显示在页面中。

我们在开发app的时候都是HybridApp开发，除了混合式之外还有web app的开发需要通过浏览器来发送数据访问，然后显示在页面中，所以需要网络。

离线存储：用户在离线状态依旧可以访问到内容，并不是每一次都需要向服务器发送请求，所以H5新增了离线存储，会把本地需要存储的内容放在扩展名为manifest的配置文件中，浏览器会根据配置文件的内容进行缓存，以供用户进行访问

* 如何使用离线存储

  需要一个后缀名为mainfest的文件，同时在html中设置manifest属性(属性：需要缓存的文件有哪些)

  **manifest文件不需要添加缓存，这个文件会自动进行存储**

```html
<html lang="en" manifest="cache.manifest">
</html>
```

* 这个文件由3部分构成

  1. cache：表示需要离线缓存的文件列表

  2. network：以下资源必须在线才能访问

     **如果在cache和network中同时加上同一个文件，那么这个文件依然会被离线存储，因为cache的优先级比network要高。**

  3. fallback：代表的是如果cache中的内容访问失败，会使用fallback里面的内容进行代替

  ```
  CACHE:
  ../js/index.js
  ../css/index.css
  ../img/1.jpg
  不同源的情况下就是一个url
  也可以直接缓存文件夹
  NETWORK:
  ../img/2.jpg
  FALLBACK:
  404.html
  ```

* 浏览器是如何对manifest文件进行解析的

  **在线**：浏览器在读取文件的时候，因为在html头部加上了manifest属性所以会请求manifest文件，如果是第一次访问这个网站，那么浏览器会根据manifest中的文件进行离线缓存

  如果访问过这个网站，那么会直接访问离线缓存中的文件，访问时会比较文件的内容，如果有更新会重新缓存文件（不管是哪个文件更新了，所有文件一起更新）。

  

  **离线**：浏览器直接访问离线缓存中的资源

## MD5加密

只能加密不能解密

先下载md5文件然后直接引入，引用完成之后直接使用，在这个文件中提供给我们一个hex_md5()进行加密的，把需要加密的内容作为方法的参数即可。



## base64

既能加密也能解密，实现加密用的是encode，实现解密用的是decode



## 管理系统：增删改查

​    把数据获取出来从接口中，然后增加数据
​    之前页面中没有数据，先从接口把数据获取出来显示再页面中，然后点击创建/添加，新增一个人（必须是自己手写得，它没在接口上），这就是增加

面试时候问你：你是怎么实现得，后台会提供给我们响应功能得接口，例如想要实现删除功能，那么先选中要删除得哪条数据，然后把当前这条数据得id值传给删除接口，这天数据就会从数据库中进行删除（调接口得目的是什么，为了操作数据库中得数据实现增删改查得功能）
前后端不分离得情况下，增删改查只能直接操作数据库来完成，都是由后台来做得
前后端分离，增删改查和原来得显示效果是不变得，操作得人变了，之前是由后台来操作得，现在由前端来操作，就是通过后台提供给我们得接口来完成的

商城得cms：商品管理、商家管理、订单管理、用户管理























## 创建对象的方法

构造函数--需要使用new进行实例化,prototype是绑定在原型上的属性,所以我们在使用的时候需要new才能获取prototype上面的属性和方法

json格式--不需要通过new进行实例化,那么prototype上边的属性就找不到



## 例题讲解知识点分析

```js
function Foo(){//this的指向：构造函数中的this指向的是window对象
  getName=function(){ //这个方法就跟私有变量一样
    console.log(1);
  };
  return this;//  没有这句话将无法调用私有变量
}
Foo.getName = function(){
  console.log(2);
};
Foo.prototype.getName=function(){//在Foo对象的原型上绑定方法，所以这个就相当于是把原来的覆盖掉了
  console.log(3);
};
var getName =function(){//在这里的考点是函数创建的方式，一种是var 变量名=function(){}-->属于变量创建方式，所以一旦创建缓存一直存在。一种是function 函数名(){}-->函数读取完直接释放缓存。如果两种创建方法同时存在得话，funtion得创建会释放，那么读取的话不会读到，直接读取的是var创建出来的全局变量。所以不会输出5
  console.log(4);
};
function getName(){
  console.log(5);
}
Foo.getName(); //不是function的原因就是，把这个foo看成是一个对象，既然是对象的话，这个对象并没有进行实例化，所以就没有
getName();//这个函数是私有函数所以找不到，可以直接访问window里面的getName这个方法
Foo().getName();//就相当于私有函数在函数内调用
getName();//因为上面的那次调用相当于把原来window里的getName重写了，因为Foo对象this是指向window的也就是说在指向问题里这个getName与全局变量getName的指向是一样的，所以会被覆盖
new Foo.getName();//把Foo看成一个构造函数，所以可以调用出来
new Foo().getName();//覆盖掉原来的内容
new new Foo().getName();//不管有几个new 都是看作一次实例化与上面的一样
```



## 实例化

new的话会进行对象的实例化

如果一个函数没有New的过程那么他单纯就是一个函数，如果有New了，那么这个对象我们可以把它看成一个构造函数，换句话来说，这里里面的this代表的就是window对象

## 创建函数的方式

函数有两种创建方式：一种是var 变量名getname=function(){}属于变量的创建方式，一旦创建缓存一直存在。一种是function getName(){}，读完之后缓存直接释放。

如果两种创建方法同时存在，function的创建会释放，那么读取的话不会读到，直接读取的是var创建出来的全局变量。

## new这个操作符具体做了哪些操作？

```js
function Foo(){}
var foo=new Foo();//这一步就是对当前Foo这个对象进行实例化出来的foo
```

1. 创建出来一个新的空对象。
2. 在继承之前会有一个this的返回，在默认的情况下自动返回的，返回到的就是实例化的这个对象上边，也就意味着这个实例化对象可以有属性有方法。
3. 把Foo父类上边的属性和方法都继承到子类foo上，在继承的过程中不管父类使用的是构造函数创建的属性和方法还是使用原型创建的属性和方法都会被子类进行继承。

这里其实可以把继承的过程看作是call继承，但是严格意义来讲是不一样的比如call是无法继承原型创建的属性和方法的，call,apply,bind()都只能继承构造函数上的属性和方法。

## 类与对象区别

类：一类事物，比如蔬菜，水果。

对象：实例化话出来的是一个具体的东西，比如土豆，芒果。

## 出现最多的字符的次数

```js
var str="ninihaoa";
var o={};
for(var i=0;i<str.length;i++){
    var char=str.charAt(i);
    if(o[char]){
        o[char]++;//次数加1
    }else{
        o[char]=1;//若第一次出现，次数记为1
    }
}
console.log(0);//输出的是完整的对象，记录着每个字符及其出现的次数
//遍历对象找到出现次数最多的字符的次数
var max=0;
for(var key in o){
    if(max < o[key]){
       max = o[key];//max始终储存最大的那个
    }
}
for(var key in o){
    if(o[key] == max){
        //console.log(key);
        console.log("最多的字符是"+key);
        console.log("出现的次数是"+max);
    }
}
```

## 千位符例题

```js
//方法一
var str="1234567";
var arr=[];
for(var i=0;i<str.length;i++){
    arr.unshift(str.substr(-3));
    str=str.substr(0,str.length-3);
}
console.log(arr.join(","));
//方法二
function parseNum(num){
    var list=new String(num).split('').reverse();
    for(var i=0;i<list.length;i++){
        if(i%4==3){
            list.splice(i,0,',');
        }
    }
    return list.reverse().join('');
}
console.log(parseNum(1234567));
```

## 原路返回例题思路

1. 事件对象，clientX和clientY
2. 每拖动一下，就产生一组x和y的值
3. 把产生的x和y的值放在数组或者是对象中，只要动一下，那么就产生一组值，每存一次就是在这个对象或者数组的后面存，所以用到push
4. 当鼠标按下并且拖动的情况下进行存值，抬起之后就不存。
5. 出来的数是点击原路返回的时候才出来。
6. 涉及到我们再次点击或者拖动的时候，所以每原路返回完成一次，就要清除掉x和y的值，这个时候使用pop，起到删除并返回数值的作用。
7. 返回的时候直接设置top和left的值

```js
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0px;
            padding: 0px;
            color: #666;
        }

        div {
            height: 150px;
            width: 300px;
            border: 1px solid #ccc;
            position: absolute;
            left: 150px;
            top: 150px;

        }

        h5 {
            line-height: 35px;
            text-align: right;
            padding-right: 12px;
            border-bottom: 1px solid #ccc;
            cursor: move;
        }

        h5 span {
            cursor: pointer;
        }

        li {
            list-style: none;
            line-height: 25px;
            padding-left: 12px;
        }
    </style>
</head>

<body>
    <div id="box">
        <h5 id="nav"><span id="back">点我原路返回</span></h5>
        <ul>
            <li>Drag: <span>false</span><>
            <li>Top: <span>150</span><>
            <li>Left: <span>150</span><>
        </ul>
    </div>
</body>
<script type="text/javascript">
    //原路返回思路：
    //1.事件对象，clientX和clientY
    //2.每拖动一下，那么就会产生一组x和y得值
    //3.我们可以把产生得这个x和y的值放在数组或者是对象中，只要动一下，那么就生成一组值，每存一次就是在这个对象或者是数组后边存得，所以用到得是push
    //4.当鼠标按下并且拖动的情况下进行存值，抬起来之后就不存了
    //5.出来的数是点击原路得返回的时候才出来
    //6.这里边涉及到我们再次点击或者拖得时候，所以每一次返回完成，之前存得x和y得值就必须删除
    //7.返回的时候直接设置top和left得值即可
    var box = document.getElementById("box"),
        nav = document.getElementById("nav"),
        back = document.getElementById("back"),
        spans = document.getElementsByTagName("span"),
        rouse = [{ x : box.offsetLeft, y : box.offsetTop }],
        Drag = false;
        nav.onmousedown = function () {
            Drag = true;
        }
    document.onmousemove = function (e) {
        var e = e || window.event;
        if (!Drag) return false;
        box.style.left = e.clientX + "px";
        box.style.top = e.clientY + "px";
        rouse.push({ x: box.offsetLeft, y: box.offsetTop });//把新获取的top和left的值存储到数组rouse中，再存得时候是从后存得所以用push
        offset();
    }
    document.onmouseup = function () {
        Drag = false;
        offset();
    }
    back.onclick = function () {
        if (rouse.length == 1) return false;//你动过了我才执行，不动我就不执行
        var timer = setInterval(function () {
            var oPos = rouse.pop();//直接从后向前进行删除就行了，删除的好处就是不用再重新把原来的rouse进行清空，{x:px,y:px}
            oPos ? (box.style.left = oPos.x + "px", box.style.top = oPos.y + "px", offset()) : clearInterval(timer)
            // if(oPos!=null){
            //     box.style.left=oPos.x + "px"
            //     box.style.top=oPos.y + "px"
            //     offset()
            // }else{
            //     clearInterval(timer)
            // }
            console.log(oPos);
        }, 3)
    }
    function offset() {  //这个方法就是为了让拖动框中得值一直变的
        spans[1].innerHTML = Drag;
        spans[2].innerHTML = box.offsetLeft;
        spans[3].innerHTML = box.offsetTop;
    }
</script>
```

## 闭包的应用

   1、可以使用闭包进行封装--选项卡、轮播图
   2、如果变量是全局变量的话，再特效里边使用的时候改变这个变量的话，会对全局变量造成污染，使用自调函数包裹起来，这样的话就不会对全局的变量造成污染
   3、可以进行缓存--为了能让别人进行访问

在使用var进行变量的创建的时候，创建出来的变量会进行提升，所以如果在其他的地方改变这个变量了，那么就会对原有的变量进行污染（全局变量），为了避免污染所以需要使用匿名自调函数进行封装

## 伪类和伪元素的区别

伪类：一般操作的时候时给页面中已有的DOM元素进行状态的改变-->a:hover,a:visited

伪元素：用于创建一些不在DOM中的元素，并且添加样式-->a:before

严格意义上来说区分伪类和伪元素的就直接是: 与 ::(仅限ie8以上的浏览器支持)



## 弹性盒子

1.CSS兼容性

* 加前缀：不同内核
* 针对IE：

2.改变弹性盒子的排列顺序使用的是flex-direction，使用的前提是必须要给最外层的元素加上flex

3.flex-warp让里面的元素放不下的话，如何换行

* no-warp不换行
* wrap换行

4.justify-content:水平对齐

* center  居中

5.align-items:垂直对齐

* center 居中

6.如果想要设置水平和垂直居中浏览器的话，从html开始，到包裹的最外层的元素，都必须加上宽高：100%

```css
html,body{
	width:100%;
	height:100%;
}
```

分界线往上都是给外边嵌套的盒子设置的


<hr></hr>
分界线往下都是给里边嵌套的盒子设置的 

7.order:数值越小越靠前显示

没有写数值的就是0

8.flex-grow：分配的是剩余空间的比例

两端固定中间自适应

9.flex-shrink:缩小的比例