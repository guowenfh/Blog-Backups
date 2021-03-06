title: JavaScript作用域学习笔记
date: 2016-07-08 00:45:23
tags: [百度前端技术学院,JS]
categories: [JS深度学习]
---


> 无论什么语言中，作用域都是一个十分重要的概念，在JavaScript中也不例外，作用域定义了变量或者函数有权访问的范围，决定了它们各自的行为。要理解JavaScript中的作用域首先就要知道：在`let`出现之前，JS中变量的作用域只有两种：全局作用域和局部作用域。（本文也只讨论这两种作用域）



### 全局作用域

全局作用域是最外围的一个执行环境，可以在代码的任何地方访问到。在浏览器中，我们的全局作用域就是`window`。因此在浏览器中，所有的全局变量和函数都是作为`window`对象的属性和方法创建的。

下面就来看看全局作用域的创建方式：

1. 全局变量与全局函数

```js
var name = "小红";
function doSomething(){
    var anotherName = "小黑";
    function showName(){
        console.info(name)
        console.info(anotherName)
    }
    showName();
}

console.info(name);//小红
console.info(anotherName);//【脚本出错】
doSomething();//小红---小黑
showName();//【脚本出错】
```
通过代码可以很清楚的看出来，我在前面所说的 **作用域定义了变量或者函数有权访问的范围** ，在这里我们定义了一个全局的变量`name`与全局函数`doSomething()`，他可以在任何地方被直接访问。但是我们又在函数内部创建了变量`anotherName`与函数`showName()`，通过代码中的调用情况可以发现，我们在外部调用它时提示【脚本出错】，因为他们处于局部作用域内（稍后讲），而 **外部环境不能访问内部环境的任何变量与函数**。这就涉及到了作用域的概念(稍后讲)

2. 未声明直接定义的变量

```js
function showName() {
    var fullName = "小红";
    anotherName = "小黑";
    console.info(fullName)
}
showName();//小红
console.info(anotherName);//小黑
console.info(fullName);//【脚本出错】
```
在这样的情况下，变量`anotherName`拥有全局作用域，而`fullName`在函数外部无法访问到。（注：在高程中明确说明，不声明而直接初始化变量是错误做法，应该避免这样的情况`严格模式下，初始化未声明的变量将报错`）

3. 所有window对象上的属性都具有全局作用

这个实际上在上面已经提到了：**所有的全局变量和函数都是作为`window`对象的属性和方法创建的。**，自然`window`对象它本身所具有的属性和方法，同样是处于全局作用域，例如：`window.location`，`window.name`等等。

### 局部作用域


其实在上面的代码中，为了展示全局作用域的效果，我们就已经创造了局部作用域。局部作用域和全局作用域正好相反，局部作用域一般只在固定的代码片段内可访问到，最常见的就是函数内部，所以在很多地方就会有人把它称为函数作用域。（记住`let`之前无块级作用域）。我们再来看一下第一段代码：

```js
var name = "小红";
function doSomething(){
    var anotherName = "小黑";
    function showName(){
        console.info(name)
        console.info(anotherName)
    }
    showName();
}
console.info(anotherName);//【脚本出错】
showName();//【脚本出错】
```
在这段代码中变量 `anotherName`,与函数 `showName()`，都拥有局部作用域。因此它不能被外部所访问，那么问题就来了，为什么全局变量他就能在局部作用域内被访问到呢？这就是 JavaScript 中的作用域链概念！

### 作用域链

在JS中:”一切皆是对象, 函数也是”。

在 JavaScript 中，每个函数都有着自己的作用域，在每次调用一个函数的时候 ，就会进入一个函数内的作用域，而当函数执行返回以后，就返回调用前的作用域。

当代码在一个作用域内执行时，就会根据其上下文创建一个作用域链，该作用域链的用途就是控制当前作用域对于内所有的变量与函数的有序访问。作用域链的最前端，始终都是当前执行代码所在的作用域的变量对象。

```js
var name = "小红";

function changeName(){
    if(name ==="小红"){
        name="小黑";
    }else{
        name ="小红";
    }
}
changeName();
console.info("新名字:"+name);//小黑
```
在这个例子中，`changName()`被定义在全局作用域下，他的作用域链包含着包含两个对象：1.它本身的变量对象(函数都会包含`arguments`对象)，2.全局环境对象。之所以能在函数内部访问到变量`name`,就是因为在它的作用域中，能找到它。（**JS的标识符解析，是沿着作用域链一级一级的查找搜索的过程，从作用域链的最前端开始直到全局环境，最终没有查找到时将报错。**）我们再回过头来稍微改一下第一段代码：并且看看他们能访问到那些变量：

```js
var name = "小红";
function doSomething(){
    var anotherName = "小黑";
    function showName(){
        var author ="三省吾身丶丶";
        console.info(name)
        console.info(anotherName)
        // 在这里可以访问到 name 、anotherName 、author
    }
    showName();
    // 在这里可以访问到 name anotherName ,不能访问到 author
}
doSomething();
// 在这里只能访问到 name
```

要想理解这种作用域其实也很简单，作用域就像是一架 **每一个台阶都是相对封闭（同级），并且只能上不能下的梯子**，在越底层的台阶上，它能走的步数越多（作用域链越长）。为了找到它想要的东西，就开始爬台阶，每爬一步台阶，都能看到这一级台阶上有什么东西，直到最顶上的那一阶。（找到了就带回去一起玩耍，玩完了之后还得换回去，要是最后都没找到就掉下去摔死了）


### 坑与示例解析

在了解坑之前，其实只要记住权威指南里面的一句话，就可以躲过很多这方面的坑了，那就是：**JavaScript中的函数运行在它们被定义的作用域里,而不是它们被执行的作用域里**

下面就来看看这一个例子：

```js
var name = '小红';
function showName() {
    console.info(name);
}

function show() {
    var name = '小黑';
    showName();
}

show();
```
结果会是什么呢？ 

```
小红
```
如果你记住并且理解了上面的话，那么应该可以得到这个结果。用作用域链的角度解析：执行`show()`函数时，进入`function show(){}`的作用域内，然后执行`showName()`函数，再进入到`function showName(){}`的作用域内，要输出`name`，就在当前作用域找，但是找不到，然后就向上爬一层，在全局环境中找到了`var name = '小红';`，所以`show()`就输出了小红。

再来看一个这个例子的改动版本

```js
var name = '小红';

function show() {
    var name = '小黑';

    function showName() {
        console.info(name);
    }
    showName();
}
show();
```
结果是：`小黑`

解析：执行`show()`函数时，进入`function show(){}`的作用域内，然后执行`showName()`函数，再进入到`function showName(){}`的作用域内，要输出`name`，就在当前作用域找，发现本身找不到，就向上爬一层到了`show()`里面，发现已经找到了`var name = '小黑';`，那么就停止查找，输出了`小黑`
。



先到这，不知道有没有对作用域有了更多的了解呢？感觉有些地方还了解的不够透彻，希望在开发项目的过程中能有更深的理解。

如果有错误之处，请指正。谢谢！
