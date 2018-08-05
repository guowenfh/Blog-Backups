title: webpack入坑之旅（二）loader入门
date: 2016-03-24 17:28:00
tags: [webpack]
categories: [前端框架]
---

这是一系列文章，此系列所有的练习都存在了我的github仓库中[vue-webpack](https://github.com/guowenfh/vue-webpack) 在本人有了新的理解与认识之后,会对文章有不定时的更正与更新。下面是目前完成的列表：

- [webpack入坑之旅（一）不是开始的开始](//guowenfh.github.io/2016/03/24/vue-webpack-01-base/)
- [webpack入坑之旅（二）loader入门](//guowenfh.github.io/2016/03/24/vue-webpack-02-deploy/)
- [webpack入坑之旅（三）webpack.config入门](//guowenfh.github.io/2016/03/24/vue-webpack-03-config/)
- [webpack入坑之旅（四）扬帆起航](//guowenfh.github.io/2016/03/24/vue-webpack-04-custom/)
- [webpack入坑之旅（五）加载vue单文件组件](//guowenfh.github.io/2016/03/25/vue-webpack-05-vue/)
- [webpack入坑之旅（六）配合vue-router实现SPA](//guowenfh.github.io/2016/03/28/vue-webpack-06-router/)


## 引子

在上一篇博客中我们已经成功的把简单的事情变得复杂了，把我们的只有几行代码的两个文件`first.js`、`entry.js`使用webpack进行文件打包生成了`bundle.js`。

`Webpack` 能做的就是这样，只能处理 JavaScript 模块。

当然它如果能做的仅仅是这样，那它也就不可能这么火了=_=。所以它可以通过引入其他的`loader`，进而可以处理其它类型的文件。

## loader介绍

`Loader`可以理解为是模块和资源的转换器，它本身是一个函数，接受源文件作为参数，返回转换的结果。这样，我们就可以通过require来加载任何类型的模块或文件，比如`VUE`、`JSX`、`SASS` 或图片。

先来看看 loader 有哪些特性？(网上复制的，不喜欢可以跳过。[loaders-地址](https://webpack.docschina.org/concepts/loaders/))

- `Loader`可以通过管道方式链式调用，每个`loader`可以把资源转换成任意格式并传递给下一个`loader`，但是最后一个`loader`必须返回JavaScript。
- `Loader`可以同步或异步执行。
- `Loader`运行在node.js环境中，所以可以做任何可能的事情。
- `Loader`可以接受参数，以此来传递配置项给`loader`。
- `Loader`可以通过文件扩展名（或正则表达式）绑定给不同类型的文件。
- `Loader`可以通过npm发布和安装。
- 除了通过`package.json`的`main`指定，通常的模块也可以导出一个`loader`来使用。
- `Loader`可以访问配置。
- 插件可以让`loader`拥有更多特性。
- `Loader`可以分发出附加的任意文件。


## loader使用

### 安装

根据上面说的`loader`的知识，就这样编译是肯定不行的，所以我们安装用来读取css文件的`css-loader`，再用 `style-loader` 把它插入到页面中。

在命令行中输入：
```sh
    npm install css-loader style-loader --save-dev
```
在`package.json`中，主要是`devDependencies`这个字段有了改变：

```json
"devDependencies": {
    "css-loader": "^0.23.1",
    "style-loader": "^0.13.0",
    "webpack": "^1.12.2"
}
```
当然你可以用一个更加方便的方式进行安装，可以直接在`package.json`中，添加相应的依赖（如上面的代码），之后的命令行中运行`npm intall`，它会自动帮我们安装相应的依赖。

安装完毕。

### 加载 CSS 文件

还是上一篇博客中的文件，来添加一个css文件。`style.css`,在里面添加

```css
body {
    background: red;
}
```
修改我们的`entry.js`，原文件不变，添加`require("!style-loader!css-loader!./style.css");`,用来引入我们的css文件。

我们继续编译:

```sh
npx webpack entry.js --output-filename=./bundle.js --mode=development
```
完成后，刷新我们的页面，背景颜色是不是已经变成了红色了呢？

### 扩展名自动绑定loader

这就是我们的`loader`的使用方式了。如果每次 `require` CSS 文件的时候都要写 `loader` 前缀`!style-loader!css-loader!`这样的东西，显然是一件很麻烦的事情。我们需要它可以根据模块类型（扩展名）来自动绑定需要的 `loader`。

来看看更简便的方式，将 `entry.js` 中的 `require("!style-loader!css-loader!./style.css") `修改为` require("./style.css") `，可以改变一个背景颜色让你更明显的查看到变化！然后执行：

```sh
npx webpack entry.js --output-filename=./bundle.js --mode=development --module-bind "css=!style-loader!css-loader"
```
。。

。。。

没成功对吧!
因为`!`在命令行中具有特殊的含义，所以我们需要对它进行转义操作。再来试试：

```sh
npx webpack entry.js --output-filename=./bundle.js --mode=development --module-bind "css=style-loader\!css-loader"
```

成功的话，应该能再次看到背景的变化。

虽然这样可以将多个css文件进行编译打包，但是总感觉很是繁琐，我不想每次都运行那么一长串的命令怎么办？继续向下走吧。
