# JS高级

## 闭包

是指**有权访问另一个函数作用域中变量的函数.**创建闭包常见的方式,就是在一个函数内部创建另一个内部(私有)函数

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
存的是匿名函数，所以每次都return i，for循环执行到3结束，并且始终都没有执行，，所以返回3
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

作业：轮播。选项卡使用闭包

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

  2.工程模式

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
console.log("person.name");
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

call apply bind只能继承构造函数里面的属性和方法

使用构造函数继承的特点:直接把父类中的属性和方法集成到自雷的构造函数中,在这个继承过程中使用call、bind()、apply

call和apply的用法是一样的，区别在于参数上边，**call的参数使用的是字符串来继承的，apply使用的是数组来继承的**

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
   Animal.call(cat,"");/使用字符串来写  继承的是Animal的属性和方法给cat
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
function test(){}
    test.prototype.sex="man";
    test.prototype.getSex=function(){
        alert(this.sex);
    }
test.prototype=new Person("");//可以获取到Person与Person.prototype上的值
var a=new test();
a.getSex();
a.getName();
```

因为对象本身有prototype这个属性和__ proto__这个隐形属性，如果想要实现原型链的话，通过的是这两个属性实现的，原型链是一种链式操作，一层一层网上找，直到到null为止

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
    //结果parent的每个实例都会聚有自己的friends属性的副本
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
//通过借用函数都有自己的属性，通过原型享用公共得犯法 console.log(result.name);
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

深拷贝：修改对对象没有影响

变就是深拷贝，不变就是浅拷贝

变量不存在深浅拷贝，只有数组和对象存在。

```js
以此为例

```

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
            if(obj.hasOwnProperty(key)){//单纯的为了判断子元素是否为对象
                 if(obj[key]&&typeof obj[key]==="object"){
            		objClone[key]=deepClone(obj[key]);//直接使用递归函数进行调用即可
        		}else{
            		objClone[key]=obj[key];//如果不是，简单复制
        		}
            }
        }
        return objClone;
}
let a=[1,2,3,4],
    b=deepClone(a);
a[0]=2;
console.log(a,b);
//不管是a也好还是b也好，他们两个指向的内存空间都是a所在的内存空间，所以a变都变
```

```js
function parseQuery(){
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
        timeout=setTime(fn,wait);
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

两种：时间戳和

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






























































