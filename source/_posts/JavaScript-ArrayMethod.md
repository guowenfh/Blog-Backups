title: JavaScript数组方法学习笔记
date: 2016-07-24 20:46:15
tags: [JS]
categories: [前端技术]
---

## 数组

> 在ECMAScript中数组是非常常用的引用类型了。ECMAScript所定义的数组和其他语言中的数组有着很大的区别。那么首先要说的就是数组也是一种对象。

> 特点:
- 在JS中,"数组"即一组数据的集合长度可变，元素类型也可以不同！
- 数组长度随时可变！随时可以修改！（length属性）


一般来说我们定义数组的方法很简单，直接使用`[]`即可，当然也可以使用`new Array()`这样的构造函数的形式，不过并不常用。对于数组本身本没有太多可以说的东西，还是直接来过一遍它的方法

### Array实例的方法

1.  `push`：向数组尾部添加元素（可多个）
```js
var arr =[];
var result = arr.push(1,true);
// arr =[1,true] 
// result=2;push方法返回值为新数组的长度
```
2.  `pop`：从数组尾部移除一个元素
```js
var arr =[1,true];
var result = arr.pop();
// arr=[1]
// result = true;pop方法返回值为被移除的元素
```
3.  `shift`：从数组头部删除一个元素
```js
var arr = [1,2,true,new Date()];
var result = arr.shift();//
// arr =[2, true, Fri May 20 2016 00:50:33 GMT+0800 (中国标准时间)] 
// result = 1;shift方法返回值为被移除的元素
```
4.  `unshift`：向数组头部添加元素（可多个）
```js
var arr = [];
var result  = arr.unshift(1,2,false);
// arr = [1, 2, false]
// result = 3 ; unshift方法返回新数组的长度
```
5.  `splice`：数组截取/插入的方法（操作数组本身）
    1.  第一个参数：截取的起始位置
    2.  第二个参数：表示截取的个数
    3.  第三个参数以后：从截取处插入新的元素（可多个）
```js
var arr = [1,2,3,4,5];
var result = arr.splice(1,2,3,4,5);
// arr = [1, 3, 4, 5, 4, 5];splice方法操作直接操作数组本身
// result = [2,3];splice方法返回被截取的元素
```
6.  `slice`：数组截取（不操作数组本身）
```js
var arr = [1,2,3,4,5];
var result = arr.slice(2,4);
// arr = [1,2,3,4,5];不操作数组本身
// result = [3,4];slice方法返回被截取的元素
```
7.  `concat`：链接两个数组的方法（不操作数组本身）
```js
var arr1 = [1,2,3];
var arr2 = [true,5];
var result = arr1.concat(arr2); 
// arr1 = [1, 2, 3];
// arr2 = [true, 5];
// result = [1, 2, 3, true, 5];concat方法返回链接后的新数组
```
8.  `join`：在每个元素之间加入内容（不操作数组本身）
```js
var arr = [1,2,3,4,5];
var result = arr.join("-");
// arr = [1, 2, 3, 4, 5];
// result = "1-2-3-4-5"; join方法返回每个元素加入内容后的字符串
```
9.  `sort`：排序（直接操作数组本身）
    -   sort方法默认按照字符串形式的utf编码进行排序，需要确切的正序或倒序排序时，需要写入自己的函数 
```js
var arr = [1,345,23,22,10,9];
var result1   = arr.sort();
// arr = [1, 10, 22, 23, 345, 9]
// result1 = [1, 10, 22, 23, 345, 9]sort方法返回排序后的数组
var result2   = arr.sort(function(a,b){
    return a-b;
});
// result2 = [1, 9, 10, 22, 23, 345];正确的从小到大排列
```
10. `reverse`：数组反转(直接操作数组本身)
```js
var arr = [12,324,543,10,9];
var result = arr.reverse();
// arr = [9, 10, 543, 324, 12];
// result = [9, 10, 543, 324, 12]; //返回反转后的数组
```
11. `indexOf`:正序查找元素的索引（0开始）
    -   只有一个参数时，表示待查找的元素
    -   两个参数时，第一个参数表示表示待查找的元素，
        第二个参数从第几个元素开始查
```js
var arr = [1,2,3,4,5,4,3,2,1];
var result1 = arr.indexOf(4)
var result2 = arr.indexOf(4,4)
// arr = [1,2,3,4,5,4,3,2,1];
// result1 = 3；返回值为查找到的元素索引
// result2 = 5
// 没有返回-1
```
12. `lastIndexOf`:倒序版本：倒序查找元素的索引（最后一个元素开始）
    -   只有一个参数时，表示待查找的元素
    -   两个参数时，第一个参数表示待查找的元素，第二个参数表示从倒数第几个元素开始查
```js
var arr = [1,2,3,4,5,4,3,2,1];
var result1 = arr.lastIndexOf(4)
var result2 = arr.lastIndexOf(4,4)
// arr = [1,2,3,4,5,4,3,2,1];
// result1 = 5；返回值为查找到的元素索引
// result2 = 3
// 没有返回-1
```
13. `forEach`：循环数组的每一个元素，并且对每一项执行一个方法。没有返回值（不操作数组本身）
```js
var arr = [1,2,3,4,5];
var result = arr.forEach(function(item,index,arr){
    return item+1; 
})
// arr = [1, 2, 3, 4, 5];
// result = undefined;forEach方法没有返回值
```
14. `map`：循环数组的每一个元素，并且对每一项执行一个方法，执行完毕后，新的数组返回（不操作数组本身）
```js
var arr = [1,2,3,4,5];
var result = arr.map(function(item,index,arr){
    return item+1; 
})
// arr = [1, 2, 3, 4, 5];
// result = [2, 3, 4, 5, 6];map方法返回运行函数后的新数组
```
15. `filter`：对于数组的每一个元素，进行一个函数的运行，给定条件去执行，返回过滤后的结果（不操作数组本身）
```js
var arr = [1,2,3,4,5];
var result = arr.filter(function(item,index,arr){
    return item>2; 
})
// arr = [1,2,3,4,5];
// result = [3,4,5];返回满足条件的值
```

16. `every`：对于数组的每一个元素都执行一个函数，如果都返回`true`,最后则返回`true`；如果有一个返回`false`,最后结果返回`false`.（不操作数组本身）
```js
var arr = [1,2,3,4,5];
var result1 = arr.every(function fun(item,index,arr){
    return item > 2;
});
var result2 = arr.every(function fun(item,index,arr){
    return item > 0;
});
// arr = [1,2,3,4,5];
// result1 = false;不全部满足条件
// result2 = true;全部满足条件
```
17. `some`：对于数组的每一个元素都执行一个函数，如果有一项返回`true`,最后则返回`true`；如果每一项返回`false`,最后结果才返回`false`.（不操作数组本身）（与上一个`every`相反）
```js
var arr = [1,2,3,4,5];
var result1 = arr.some(function fun(item,index,arr){
    return item>=5;
});
var result2 = arr.some(function fun(item,index,arr){
    return item<0;
});
// arr = [1,2,3,4,5];
// result1 = true;不全部满足条件
// result2 = false;每一项都返回false
```
18. `reduce`:最终构建一个返回值，接收一个函数作为累加器（accumulator），数组中的每个值（从左到右）开始合并，最终为一个值。
```js
var arr = [1,2,3,4,5];
/**
 * perv:前一个值
 * cur：当前值
 * index：当前索引位置
 * arr：原数组
 **/
var result = arr.reduce(function(perv,cur,index,arr){
    return perv +cur;
});
// arr = [1,2,3,4,5];
// result = 15;
```
19. `reduceRight`:倒序版本：最终构建一个返回值，
遍历的起始位置不同
```js
var arr = [1,2,3,4,5];
/**
 * perv:前一个值
 * cur：当前值
 * index：当前索引位置
 * arr：原数组
 **/
var result = arr.reduceRight(function(perv,cur,index,arr){
    return perv +cur;
});
// arr = [1,2,3,4,5];
// result = 15;
```
