title: HTML5常用标签分类
date: 2017-04-21 23:45:12
tags: [HTML]
categories: [前端技术]
---

> 文章是很早之前的笔记，做了一些属性上的补充，现发布到博客中来

[十年踪迹的博客：HTML5 元素选择流程图](https://www.h5jun.com/post/html5-element-flowchart.html?utm_source=tuicool&utm_medium=referral)
<img src="https://p3.ssl.qhimg.com/t01d712cd34f492117d.png" class="full-image" art="如何选择标签"/>

<!--more-->

HTML5基本介绍

**HTML5 设计思想**
- 兼容已有内容
- 避免不必要的复杂性
- 解决现实的问题
- 优雅降级
- 尊重事实标准
- 用户－>开发者－>浏览器厂商－>标准制定者－>理论完美

**语法**
- 标签不区分大小写，推荐小写
- 空标签可以不闭合，比如 input / meta
- 属性不必引号，推荐双引号
- 某些属性值可以省略，比如 required,readonly

-----

HTML5常用标签分类



### 一. HTML文档标签

1. `<!DOCTYPE>`: 定义文档类型.
2. `<html>`: 定义HTML文档.
3. `<head>`: 定义文档的头部.(头部内包含)
4. `<meta>`: 定义元素可提供有关页面的元信息，比如针对搜索引擎和更新频度的描述和关键词(由于规范没有规定关于 mete 中各种属性的强制定义，所以不同的浏览器都都可以通过 mete 来声明一些规则)
    - 参考：[移动端的头部标签](https://github.com/yisibl/blog/issues/1)
    - `<meta charset ="UtF-8">`
    - `<meta name ="keywords" conten="关键词">`
    - `<meta name ="description" conten="页面介绍">`
    - `<meta name =" viewport" conten="initial-scale=1">`
5. `<base>`:定义页面上的所有链接规定默认地址或默认目标.
6. `<title>`: 定义文档的标题.
7.  `<link>`: 定义文档与外部资源的关系.
8.  `<style>`:定义 HTML 文档样式信息.
9. `<body>`: 定义文档的主体.(脚本在非必须情况时在主体内容最后)
10. `<script>`: 定义客户端脚本，比如 JavaScript.
11. `<noscript>`:定义在脚本未被执行时的替代内容.（文本）

### 二. 布局标签&语义化

![](https://ws1.sinaimg.cn/large/82d12951gy1fevim1rbn6j20zq0tyjum.jpg)

1. `<div>`:定义块级元素.
2. `<span>`:定义行业元素.
3. `<header>`5[^footnote]:定义区段或页面的页眉.(头部)
4. `<footer>`:定义区段或页面的页脚.(足部)
5. `<section>`:定义文档中的区段.
6. `<article>`:定义文章.（在`<article>`中也可以进行内容划分）
    -   ![](https://ws1.sinaimg.cn/large/82d12951gy1fevim24vmpj20n40lsgpn.jpg)
7. `<aside>`:定义页面内容之外的内容.
8. `<details>`:定义元素的细节.
9. `<summary>`:定义 `<details>` 元素可见的标题.
10. `<dialog>`:定义对话框或窗口.
11. `<nav>`:定义导航.
12. `<hgroup>`:定义标题组

### 三. 表格标签

1. `<table>`:定义表格.
    - `border=1`定义边框
2. `<caption>`:定义标题.（规范：必须是 table 的第一个元素）
3. `<thead>`:定义页眉.
4. `<tbody>`:定义主体.
5. `<tfoot>`:定义页脚.
6. `<th>`:定义表头.
7. `<tr>`:定义一行.
8. `<td>`:定义单元格.
    - `rowspan="2"`跨行（竖直）
    - `colspan="2"`跨列（水平）
9. `<colgroup><col class="" span="2"></colgroup>`:列组,批量的给列做处理
### 四. 表单标签

1. `<form>`:定义表单.(表单包含在form标签中)
    - `novalidate`:禁用原生的验证规则
    - 表单提交最好是绑定 submit 事件
2. `<input>`:定义输入域.
    - `name="username"`：原生表单提交用于传输的 key 例：key1=value1&key2=value2
    - `placeholder="2-10位"`：描述文字
    - `minlength="2"`最少（记录一下，一般这些还是走 js）
    - `maxlength="10"`：最多
    - `required`：是否必填
    - `pattern="1\d{10}"`：正则表达式
    - `type="text"`：input 类型如 search/number/email等都是输入
    - `readeonly`
    - `disabled`
3. `<textarea>`:定义文本域.(多行)
4. `<label>`:定义一个控制的标签.(input 元素的标注)
    - `for="abc"`, abc 为一个 id="abc"的标签
    - 如果直接把 input 整个包在 label 中也可以有 for 的效果
5. `<fieldset>`:定义域.
6. `<legend>`:定义域的标题.
7. `<select>`:定义一个选择列表.
    - `name="aaaa"`：原生表单提交用于传输的 key
    - `size="3"`:只展示几个
    - `multiple`：是否开启多选
8. `<optgroup>`:定义选择组.
9. `<option>`:定义下拉 列表的选项.
10. `<button>`:定义按钮.
    - `type="submit"`:默认的是 submit
    - `type="button"`：大部分时间都会手动设置
    - `type="reset"`：重置
11. `<fieldset>`:定义围绕表单中元素的边框.
12. `<legend>`:定义 fieldset 元素的标题.
13. `<fieldset>`:定义选项列表.与input 元素配合使用该元素，来定义 input 可能的值.
14. `<keygen>`:定义表单的密钥对生成器字段.
15. `<output>`:定义不同类型的输出，比如脚本的输出.

### 五. 列表标签
列表相关的标签，需要注意其嵌套规则
1. `<ul>`:定义无序列表.
2. `<ol>`:定义有序列表.
    - 属性 `start＝"1"` 表示开始位置
3. `<li>`:定义列表项.
4. `<dl>`:定义自定义列表.
5. `<dt>`:定义自定义列表项.
6. `<dd>`:定义自定义的描述.

### 六. 图像&链接标签

1. `<img>`:定义图像.
    - `alt="替代文字"`：必须加！
    - `height="200" width="300"`，可用 css 指定
    - 不指定宽高：原图大小显示
    - 指定宽度：按比例缩放到指定宽度
    - 指定高度：按比较缩放到指定高度
    - 指定宽高：强制按指定宽高显示
2. `<a>`:定义超链接.
    - `href="url"`在这里链接有多种形式
    - 省略协议：`href="//baidu.com"`，自动根据当前页面协议补充
    - 省略协议和host(同时支持相对与绝对路径):`href="/index.html"`
    - 页面内链接（锚点）：`href="#test"`会找到页面中id 或者name 为test 的元素
    - 链接目标：`target="_self"`（当前窗口）`_blank`(新窗口) `abc`(开一个自定义窗口名称)
3. `<map>`:定义图像映射。
4. `<area>`:定义图像地图内部的区域.
5. `<figure>`:定义媒介内容的分组.（图表，图片，一段代码等）描述`<img>`内容等。
6. `<figcaption>`:定义 `<figure>` 元素的标题.

### 七. 音频/视频

1. `<audio>`:定义声音内容.
2. `<source>`:定义媒介源.
3. `<track>`:定义用在媒体播放器中的文本轨道.
4. `<video>`:定义视频.

### 八. 框架标签
1. `<iframe>`:内联框架.

### 九.格式标签
#### 1. 文章标签
1. `<h1>`-`<h6>`:定义 HTML 标题.
2. `<p>`:定义段落.
3. `<br>`:定义换行.
4. `<hr>`:定义水平线.
5. `<bdo>`:定义文字方向.
6. `<pre>`:定义预格式文本.保留换行等格式
7. `<abbr>`:定义缩写.
8. `<address>`:定义文档作者或拥有者的联系信息.
9. `<ins>`:定义被插入文本.（比如博客中时效性的语句）
10. `<del>`:定义被删除文本.
11. `<time>`:定义日期/时间.
12. `<wbr>`:定义虚拟的空格换行（例如长段的url）
#### 2. 短语元素标签

1. `<dfn>`:定义定义项目.
2. `<code>`:定义代码（长短都可）
3. `<samp>`:定义计算机代码样本.
4. `<kbd>`:定义键盘文本.
5. `<var>`:定义文本的变量部分.
6. `<sup>`:定义上标文本.
7. `<sub>`:定义下标文本.
8. `<cite>`:定义引用.（标题/章节/书名）等
9. `<blockguote>`:定义长的引用.
    - 属性：`cite="url"` 表示引用来源
10. `<q>`:定义短的引用.（一句话等）

#### 3. 字体样式标签
1. `<em>`:定义强调文本.（从一句话中突出某个词语）
2.  `<strong>`:定义语气更为强烈的强调文本.（重要性，严重性和紧急性）
3. `<i>`:显示斜体文本效果.（换一种语调去说已句话时，比如其他语言翻译，对话中的旁白）
4. `<b>`:呈现粗体文本效果.（将词语从视觉上和其他部分区分，比如一篇论文摘要中的关键词）
5. `<big>`:呈现大号字体效果.
6. `<small>`:呈现小号字体效果.
7. `<mark>`:定义有记号的文本.（和用户当前行为相关的突出，比如在搜索中匹配到的次，或者一部分内容需要在后面引用时）

###  十. 其它

1. `<canvas>`:定义图形容器，必须使用脚本来绘制图形。
2. `<meter>`:定义预定义范围内的度量.
3. `<progress>`:定义任何类型的任务的进度.

### 十一. 一些 HTML全局属性
- accesskey：键盘快捷键
- id
- class
- style
- title
- hidden：标签隐藏
- lang：语言类型:'en','zh-CN'
- dir:文本排列方向
- tabindex
- contenteditable：内容编辑
- spellcheck:拼写检查
