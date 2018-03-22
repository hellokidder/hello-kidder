# this

this提供了一种更优雅的方式来隐式“传递”一个对象的引用，因此可以将API设计的更简洁并且易于复用

### 关于this的误解
- 指向自身

```
function foo(num) {
  console.log("foo:"+num);//记录foo被调用的次数
  this.count++;
}
foo.count = 0;
var i;
for(i=0;i<10;i++){
  if(i > 5){
    foo(i)
  }
}
// foo:6
// foo:7
// foo:8
// foo:9
// foo被调用的次数
console.log(foo.count);// 0?
```
执行foo.count = 0时，的确向函数对象foo中添加了一个属性count，但是函数内部代码this.count中的this并不是指向那个函数对象，所以虽然属性名相同，根对象却并不相同

强制this指向foo函数对象：
```
function foo(num) {
  console.log("foo:"+num);//记录foo被调用的次数
  this.count++;
}
foo.count = 0;
var i;
for(i=0;i<10;i++){
  if(i > 5){
    foo.call(foo,i)//使用call(..)可以确保this指向函数对象foo本身
  }
}
// foo:6
// foo:7
// foo:8
// foo:9
// foo被调用的次数
console.log(foo.count);// 4
```
- 它的作用域

第二种常见的误解，this指向函数的作用域，这个问题有点复杂，因为在某种情况下它是正确的，但在其它情况下它确实错误的。

> 需要明确的是，this在任何情况下都不指向函数的词法作用域。在JavaScript内部，作用域确实和对象类似，可见的标识符都是它的属性。但是作用域“对象”无法通过JavaScript代码访问，它存在于JavaScript引擎内部

看代码：
```
function foo() {
    var a = 2;
    this.bar();
}
function bar() {
    console.log(this.a);
}
foo();//ReferenceError:a is not defined
```
首先，这段代码试图通过this.bar来引用bar()函数。这样调用能成功纯属意外，调用bar()最自然的方法是省略前面的this,直接使用词法引用标识符。

此外，编写这段代码的开发者还试图使用this联通foo()和bar()的词法作用域从而让bar()可以访问foo()作用域里的变量a。这是不可能实现的

>this是在运行时进行绑定的，并不是在编写时绑定，它的上下文取决于函数调用时的各种条件，this的绑定和函数声明的位置没有任何关系，只取决于函数的调用方式
---
### 调用位置

```
function baz() {
  //当前调用栈：baz
  //当前调用位置在全局作用域
  console.log("baz");
  bar();<--bar的调用位置
}
function bar() {
  //当前调用栈：baz->bar
  //当前调用位置在baz中
  console.log("bar");
  foo();<--foo的调用位置
}
function foo() {
  //当前调用栈：baz->bar->foo
  //当前调用位置在bar中
  console.log("foo");
}
baz();<--baz的调用位置
```
分析调用栈，调用位置就在当前正在执行的函数的**前一个**调用中

---

### 绑定规则
##### 1. 默认绑定
独立函数调用（可以把这条规则看作是无法应用其它规则时的默认规则）
```
function foo() {
  console.log( this.a );
}
var a = 2;
foo();// 2
```
调用foo()时this.a被解析成全局变量a，函数调用时应用了this的默认绑定，因此this指向全局对象
> 代码中，foo()是直接使用不带任何修饰的函数引用进行调用的，因此只能使用默认绑定

**注意**：如果使用严格模式（strict mode），则不能将全局对象用于默认绑定，因此this会被绑定到undefined

##### 2.隐式绑定
调用位置是否有上下文对象，或者说是否被某个对象拥有或者包含
```
function foo() {
  console.log( this.a );
}
var obj = {
  a:2,
  foo:foo
}
obj.foo();//2
```
foo()被调用时obj对象“包含”它，当函数引用有上下文对象时，隐式绑定规则会把函数调用中的this绑定到这个上下文对象。
> 对象属性引用链只有最后一层在调用位置中起作用

```
function foo() {
  console.log( this.a );
}
var obj2 = {
  a:42,
  foo:foo
}
var obj1 = {
  a:2,
  obj2:obj2
}
obj1.obj2.foo(); //42
```
**隐式丢失**

一个常见的this绑定问题就是被隐式绑定的函数会丢失绑定对象，也就是说它会应用默认绑定，从而把this绑定到全局对象或者undefined上，取决于是否是严格模式(严格模式绑定到undefined上)
```
function foo() {
  console.log( this.a );
}
var obj = {
  a:2,
  foo:foo
}
var bar = obj.foo;//函数别名
var a = "hello Kidder!";//a是全局对象
bar();//严格模式下输出undefined，非严格模式输出“hello Kidder!”
```
虽然bar是obj.foo的一个引用，但实际上，它引用的是foo函数本身，因此此时的bar()其实是一个不带任何修饰的函数调用，因此应用了**默认绑定**

```
function foo() {
  console.log( this.a );
}
function doFoo(fn){
  //fn其实引用的是foo
  fn();//<--调用的位置
}
var obj = {
  a:2,
  foo:foo
}
var a = "hello Kidder!";//a是全局对象的属性
doFoo(obj.foo);//严格模式下输出undefined，非严格模式输出“hello Kidder!”
```
参数传递其实就是一种隐式赋值，因此传入函数时也会被隐式赋值，所以结果跟上个例子一样

如果把函数传入语言内置的函数而不是传入你自己声明的函数，结果是一样的
```
function foo() {
  console.log( this.a );
}
var obj = {
  a:2,
  foo:foo
}
var a = "hello Kidder!";//a是全局对象的属性
setTimeout(obj.foo,1000);//严格模式下输出undefined，非严格模式输出“hello Kidder!”
```
回调函数丢失this绑定是非常常见的，此外，调用回调函数的函数可能会出乎我们意料的修改this

##### 3.显示绑定
```
function foo() {
  console.log( this.a );
}
var obj = {
  a:2
}
foo.call(obj);// 2
```
通过foo.call(..)可以在调用foo时强制把它的this绑定到obj上。

但是，显示绑定仍然无法解决我们之前提出的丢失绑定的问题

**硬绑定**
但显示绑定的一个变种可以
```
function foo() {
  console.log( this.a );
}
var obj = {
  a:2
}
var bar = function() {
  foo.call(obj);
};
bar(); //2
setTimeout(bar,1000);
//硬绑定的bar不可能再修改它的this
bar.call(window);
```
我们创建了bar（）函数，并且在它的内部手动调用了foo.call(obj),因此强制把foo的this绑定到了obj.无论之后如何调用函数bar，它总会手动在obj上调用foo.这种绑定是一种显示的强制绑定，因此称为硬绑定

- 硬绑定的典型应用场景就是创建一个包裹函数，负责接收参数并返回值
```
function foo(something) {
  console.log( this.a,something );
  return this.a + something;
}
var obj = {
  a:2
};
var bar = function() {
  return foo.apply(obj,arguments);
};
var b = bar(3);//2 3
console.log(b);//5
```
- 另一种使用方法是创建一个可以重复使用的辅助函数
```
function foo(something) {
  console.log( this.a,something );
  return this.a + something;
}
//简单的辅助绑定函数
function bind(fn,obj) {
  return function() {
    return fn.apply(obj,arguments);
  };
}
var obj = {
  a:2
};

var bar = bind(foo,obj);

var b = bar(3);//2 3
console.log(b);//5
```
由于硬绑定是一种非常常用的模式，所以ES5提供内置的方法Function.prototype.bind,它的用法如下：
```
function foo(something) {
  console.log( this.a,something );
  return this.a + something;
}
var obj = {
  a:2
};

var bar = foo.bind(obj);

var b = bar(3);//2 3
console.log(b);//5

```
bind(..)会返回一个硬编码的新函数

**API调用的上下文**

第三方库的许多函数，以及JavaScript语言和宿主环境中许多新的内置函数，都提供了一个可选的参数，通常成为“上下文”（context）,其作用和bind(..)一样，确保你的回调函数使用指定的this
```
function foo(el) {
  console.log(el,this.id);
}
var obj = {
  id:"awesome"
};
// 调用foo(..)时把this绑定到obj
[1,2,3].forEach(foo,obj);
//1 'awesome' 2 'awesome' 3 'awesome'
```

##### 4.new绑定

在JavaScript中，构造函数只是一些使用new操作符时被调用的函数。它们并不属于某个类，也不会实例化一个类，实际上，他们甚至不能说是一种特殊的函数类型，它们只是被new操作符调用的普通函数而已

> 包括内置对象函数（比如Number(..)）在内的所有函数都可以用new来调用，这种函数调用被称为构造函数调用。这里有一个重要但是非常细微的区别：实际上并不存在所谓的“构造函数”，只有对函数的“构造调用”。

使用new来调用函数，或者说发生构造函数调用时，会自动执行下面的操作
1. 创建（或者说构造）一个全新的对象
2. 这个新对象会被执行[[Prototype]]连接
3. 这个新对象会绑定到函数调用的this
4. 如果函数没有返回其它对象，那么new表达式中的函数调用会自动返回这个新对象
 
```
function foo(a) {
  this.a = a;
}
var bar = new foo(2);
console.log(bar.a);// 2
```
使用new来调用foo(..)时，我们会构造一个新对象并把它绑定到foo(..)调用中的this上。new是最后一种可以影响函数调用时this绑定行为的方法，我们称之为new绑定

---
### 优先级

**隐式绑定和显示绑定**
```
function foo() {
  console.log(this.a);
} 

var obj1 = {
  a:2,
  foo:foo
};
var obj2 = {
  a:3,
  foo:foo
};

obj1.foo();//2
obj2.foo();//3

obj1.foo.call(obj2);//3
obj2.foo.call(obj1);//2
```
可以看到显示绑定比隐式绑定优先级更高

**new绑定和隐式绑定**
```
function foo(something) {
  this.a = something
} 

var obj1 = {
  foo:foo
};
var obj2 = {};

obj1.foo(2);
console.log(obj1.a);//2

obj1.foo.call(obj2,3);
console.log(obj2.a);//3

var bar = new obj1.foo(4);
console.log(obj1.a);//2
console.log(bar.a);//4
```
new绑定比隐式绑定优先级更高

**new和显示绑定不能直接比较，比较new和硬绑定**

new 和 call/apply无法一起使用

```
function foo(something) {
  this.a = something
} 

var obj1 = {};

var bar = foo.bind(obj1);
bar(2);
console.log(obj1.a);//2

var baz = new bar(3);
console.log(obj1.a);//2
console.log(baz.a);//3
```
......

new的优先级比显示绑定更高

**判断this**

1. 函数是否在new中调用？ 如果是的话，this绑定的对象是新创建的对象
2. 函数是否通过call/apply或者硬绑定调用？this绑定的是指定的对象
3. 函数是否在某个上下文中调用？this绑定的是那个上下文对象
4. 都不是，严格模式绑定到undefined，否则绑定到全局对象
 
---
### 绑定例外

- 如果你把null或者undefined作为this的绑定对象传入call,apply,bind，这些值在调用时会被忽略，实际应用的是默认绑定
```
function foo() {
  console.log(this.a);
}

var a = 2;

foo.call(null);//2或undefined
```
应用：

一种常见的做法是使用apply(..)来“展开”一个数组，并当做参数传入一个函数。类似的，bind(..)可以对参数进行柯里化，这种方法有时非常有用
```
function foo(a,b) {
  console.log("a:" + a + "，b:" + b);
}
//把数组展开
foo.apply(null,[2,3]);//a:2，b:3
//使用bind进行柯里化
var bar = foo.bind(null,2);
bar(3);//a:2，b:3
```
然而，总是使用null来忽this绑定可能会产生某些副作用。。。。。。

更安全的方法：

创建一个空对象最简单的方法Object.create(null),Object.create(null)和{}很像，但是并不会创建Object.prototype这个委托，所以它比{}“更空”：

```
function foo(a,b) {
  console.log("a:" + a + "，b:" + b);
}
// ø =>option+o
var ø = Object.create(null);
//把数组展开
foo.apply(ø,[2,3]);//a:2，b:3
//使用bind进行柯里化
var bar = foo.bind(ø,2);
bar(3);//a:2，b:3
```
- 你有可能有意或无意的创建一个函数的“间接引用”，这种情况下，调用这个函数会应用默认绑定

间接引用最容易在赋值时发生
```
function foo() {
  console.log(this.a);
}
var a = 2;
var o = {
  a:3,
  foo:foo
};
var p = { a:4 };

o.foo();//3
(p.foo = o.foo)();//2或undefined
```

赋值表达式p.foo = o.foo 的返回值是目标函数的引用，因此调用位置是foo()而不是p.foo()或者o.foo().

- 软绑定

硬绑定会大大降低函数的灵活性，使用硬绑定后就无法使用隐式绑定或者显示绑定来修改this.

如果可以给默认绑定制定一个全局对象和undefined以外的值，那就可以实现和硬绑定相同的效果，同时保留隐式绑定或者显示绑定修改this的能力

可以通过一种叫软绑定的方法来实现我们想要的效果：

```
if(!Function.prototype.softBind) {
  Function.prototype.softBind = function(obj) {
    var fn = this;
    //捕获所有curried参数
    var curried = [].slice.call(arguments,1);
    var bound = function() {
      return fn.apply(
        (!this||this ===(window||global))?obj:this,
        curried.concat.apply(curried,arguments)
      );
    };
    bound.prototype = object.create(fn.prototype);
    return bound;
  };
}
```
```
function foo() {
  console.log("name:" + this.name);
}

var obj = {name:"obj"},
    obj2 = {name:"obj2"},
    obj3 = {name:"obj3"};

var fooOBJ = foo.softBind(obj);
fooOBJ(); //name:obj

obj2.foo = foo.softBind(obj);
obj2.foo(); //name:obj2

fooOBJ.call(obj3);//name:obj3

setTimeout(obj2.foo,10);//name:obj

```

---
### this词法

特殊函数类型：箭头函数

箭头函数并不是使用function关键自定义的，而是使用被称为“胖箭头”的操作符=>定义的。箭头函数不使用this的四种标准规则，而是根据外层（函数或全局）作用域来决定this

```
function foo() {
  //返回一个箭头函数
  return (a) => {
    console.log(this.a);//this继承自foo
  };
}

var obj1 = {
  a:2
};

var obj2 = {
  a:3
};

var bar = foo.call(obj1);
bar.call(obj2);//2,不是3！

```
foo()内部创建的箭头函数会捕获调用时foo()的this。由于foo（）的this绑定到obj1，bar(引用箭头函数)的this也会绑定到obj1，箭头函数的绑定无法被修改（new也不行）

箭头函数常被用于回调函数中：
```
function foo() {
  setTimeout(()=>{
    console.log(this.a);//这里的this在词法上继承自foo()
  },1000);
}

var obj = {
  a:2
};

foo.call(obj);
```

虽然self = this 和箭头函数看起来都可以取代bind(..),但本质上来说它们想代替的是this机制s