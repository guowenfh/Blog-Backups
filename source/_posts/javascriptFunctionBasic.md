title: JavaScript函数学习笔记
date: 2016-07-31 20:03:45
tags: [百度前端技术学院,JS]
categories: [JS深度学习]
---

## 函数 

> 函数式一块javascript代码，定义一次，可以被多次调用与执行，JS中的函数也是对象，所以JS函数可以像其他对象那样操作，和传递，所以也称函数对象
> 函数的参数列表相当于函数的人口，`return`相当于函数的出口，函数本身就是一种数据类型，函数是可以嵌套定义的。

### 函数基础

####　定义函数的方式

有三种方式可以定义函数。并且有着如下区别：

| 定义方式： | `function` 语句（函数声明） | `Function` 构造函数 | 函数表达式|
|----|---|----|------|
| 解析时机： | 优先解析(声明前置) | 顺序解析 | 顺序解析(声明提前，赋值不提前) |
| 允许匿名： | 有名 | 匿名 | 匿名|
| 形式： | 句子 |表达式 | 表达式 |
| 性质： | 静态 | 动态 | 静态|
| 作用域： | 具有函数的作用域 | 顶级函数(顶级作用域)| 具有函数作用域 |

主要有下面两个需要注意的地方：

- 理解`Function` 构造函数的顶级作用域，直接看代码就好：很直观就可以表示出来

```js
var a = 1;
function test() {
    var a  = 2;
    var func = new Function("console.info(a)");
    func();
}
test();//1;
```

- 函数表达式的多种创建方式：

```js
// 最简单的形式，将函数赋值给一个变量
var add = function(a,b){
    //do ..
}
// 立即执行匿名函数表达式IIFE
(function() {
    //do ..
})();
// 将函数当成返回值
return function(){
    //do ..
}
//命名式函数表达式NFE
var add  = function foo(a,b){
    // do..
    // 只在foo函数内部可以使用foo这个名称(用途如：递归调用)（在新版浏览器下可用）
    // 外部访问不到foo这个函数名
}
```


#### 函数的参数

> 在JS中函数的参数分为形式参数和实际参数两个概念

```js
function test(a,b,c,d) {
    console.log(test.length)//4
    return a+b+c;
}
console.info(test(10,20,30))//60
console.log(test.length)//4
console.log(arguments.length);//3,表示实际接受的参数个数
console.log(arguments[0]);//10，传进来的第一个参数===a
```

在 **函数内部** ，JS使用了一个特别的变量`arguments`的 **类数组对象**（以后再来说这个问题），用来接受传入函数的实际参数列表。

```js
function arg(a,b,c){
    arguments[0] = 1;
    console.info(a,b,c)
}
arg(143,456,6)//1 456 6
```
普通模式下可以直接对于`arguments`对象进行更改，上面的代码就是一个很直观的例子，我们直接更改了第一个参数的值，**但建议不要去试图更改`arguments`对象的属性**，不符合规范。
注：严格模式下`arguments`对象是实参的一个副本，所以上面的改动不会生效(自行尝试)


### 构造函数

什么是构造函数？

其实构造函数只是普通函数的一个变种，它可以当成普通的函数方式调用，也能通过`new`关键字来调用。 在`Javascript`中通过 `new` 关键字方式调用的函数都被认为是构造函数。
在构造函数内部（ 也就是被调用的函数内） `this` 指向新创建的对象`Object`。 这个新创建的对象的 `prototype` 被指向到构造函数的 `prototype`。
如果被调用的函数没有显式的 `return` 表达式，则隐式的会返回 `this` 对象(也就是新创建的对象)。

这就来看看实际中不同情况下的区别：

1. 使用`new`关键字吗，不指定`return`语句

```js
function Person() {
    this.father = 'allen';
}
Person.prototype.getFatherName = function(){
    console.info(this.father);
};
var hong = new Person();
console.info( new Person());//Person {father: "allen"}
hong.getFatherName();//allen
```
2. 使用`new`关键字，并且指定`return`语句

```js
function Person() {
    this.father = 'allen';
    return "1";
}
Person.prototype.getFatherName = function(){
    console.info(this.father);
};
var hong = new Person();
console.info( hong);//Person {father: "allen"}
hong.getFatherName();//allen

//把return的值换成一个对象：
//return "1";----------->return {a:1};或者return new String("12");
var hong = new Person();
console.info( hong);//Object {a: 1}
hong.getFatherName();//[脚本错误]
```
3. 不使用`new`关键字，当成普通函数直接调用

```js
function Person() {
    this.father = 'allen';
    return function(){
        return {}
    };
}
Person.prototype.getFatherName = function(){
    console.info(this.father);
};
var bai = Person();
console.info(bai);//undefined
console.info(father);//allen
bai.getFatherName();//[脚本错误]
```


通过这三段不同情况的示例代码，应该可以发现一些区别：

1. 使用`new`关键字吗，不指定`return`语句时，将隐式的会返回 `this` 对象(返也就是新创建的对象)。
2. 使用`new`关键字，并且指定`return`语句时，需分为两种情况：
    - 返回值为标准类型，显式的 `return` 表达式将**不会**影响返回结果
    - 返回值为对象，将直接返回你显式设置的对象
3. 不使用`new`关键字，当成普通函数直接调用时，`this`指向全局对象 window，所以内部this指定的属性与方法，全部都暴露到全局，导致全局变量污染。prototype上的方法不起效果(当然你要是这样的形式指定了return返回的内容，它自然会原样返回啦！)

#### 工厂模型

为了不使用`new`关键字，构造函数必须显式的返回一个值。

```js
function createPerson(name, age, sex) {
    var obj = {};
    obj.name = name;
    obj.age = age;
    var private = 2;//私有外部不可访问
    obj.sayName = function(){
        console.info(this.name)
    }
    obj.getPrivate = function() {
        return private;
    }
    return obj;
}
var p1 = createPerson("小红",21,"女")
var p2 = createPerson("小国",22,"男")
console.info(p1.name);//小红
console.info(p2.age);//22
p2.sayName();//小国
```
这就是一个简单的工厂模型，使用或者不使用` new `关键字没有功能性的区别。这样的方式比起 `new`的调用方式不容易出错，并且可以充分利用 **私有变量**带来的便利， 但是也有下面这样的问题

1. 占用更多的内存，因为新创建的对象不能共享原型上的方法。
2. 为了实现继承，工厂方法需要从另外一个对象拷贝所有属性，或者把一个对象作为新创建对象的原型。

这一篇博客最主要是对于函数学习的笔记，不过用自己的话来描述总描述的还不够清晰。
有错误之处请指出！
