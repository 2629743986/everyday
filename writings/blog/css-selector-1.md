##前言
前几天整理了CSS一些技术关键字，但是因为自己的知识过于单薄，觉得考虑的不充分有欠缺，随后便在sf.gg提出了这个问题《[关于CSS核心技术关键字都有哪些？][1]》，也是为了让厉害的人一起参与进来，用他们的经验告知我们CSS中哪一块的知识点是重要，或者说是不可欠缺的，也或者说是应该打好基础的。

在整理这份CSS技术关键字的开始，首先想到的是选择器，它作为最常用的的一个特性，几乎天天都在使用，但是如果让你说出20种CSS选择器，是不是可以脱口而出呢？ 哎，或许我们被浏览器逼的还停留在CSS2.1那些选择器把？CSS4规范都要问世了，我们还在玩那个？ 

![clipboard.png](/img/bVm2Al)

带着这些疑问，决定梳理一下之前用到的知识点，最终以系列文章的方式说一说我对选择器的理解，具体包含的内容如下：

* 选择器的基础使用，主要是CSS3，也会介绍新增CSS4选择器，包括各浏览器对选择器的支持情况
* 选择器的使用技巧，使用时常出现的一些问题，扒一扒解决方案，再说一说效率和优化的部分
* 选择器的优先级，理一理比较头疼的权重问题，如何更轻松的理解它


##导图与源码
我在写这篇文章的时候会梳理一份思维导图，用于更加直观的查阅所有的CSS选择器，并且也有编写示例代码，更方便理解文章中的示例。

关于思维导图和示例代码，会上传至Github，当然也会随着时间的允许，不定义补充和更新
仓库地址：[https://github.com/Alsiso/everyday][2]
思维导图：https://github.com/Alsiso/everyday/blob/master/codes/css-selectors/css-selectors.png
示例代码：https://github.com/Alsiso/everyday/tree/master/codes/css-selectors

关于`everyday`是我每天记录和总结的地方，这里有代码，布局方案，移动端适配方案等等，后续会不断的补充和更新，欢迎一起聊代码，玩前端。


![clipboard.png](/img/bVm7IJ)




##基本选择器

### 通配符选择器 `*`
通配符选择器用来选择所有的元素

```
* {
    marigin: 0;
    padding: 0;
}
```
在我之的文章中讨论过[CSS RESET][3]，其中里面的核心代码就是使用通配符选择器定义的，来重置浏览器所有元素的内边距和外边距。

其实，通配符选择器还可以选择某一个元素下的所有元素 
```
#demo *{
    margin:0;
}
```

不过使用通配符要**谨慎**，并不是因为[通配符会带来性能问题][4]，而是滥用通配符会造成[“继承失效”或“继承短路”][5]的问题，这种情况会对开发造成一定程度的影响。


### 元素选择器 `E`
元素选择器使用也很简单，它用于指定HTML文档中元素的样式

``` 
ul{
    list-style:none;
}
```
▲ 这里使用**元素选择器**选择`ul`元素并去除列表前面的默认圆点

### 类选择器`.className`
类选择器是最常用的一种选择器，使用时需要在HTML文档元素上定义类名，然后与样式中的`.className`相匹配，它一次定义后，在HTML文档元素中是可以**多次复用**的。

**CSS**
```
.menu {
    margin:0 auto;
}
```

**HTML**
```
<div class="menu"></div>
```

类选择器还可以**结合元素选择器**来使用，假设文档中有两个元素都使用了`.menu`类名，但是你只想选择`div`元素上类名为`.menu`的元素

**CSS**
```
div.menu {
    margin:0 auto;
}
```

**HTML**
```
<div class="menu"></div>
<ul class="menu"></ul>
```

**类选择器支持多类名使用**，比如`.menu.active`这个选择器只对元素中同时包含了`menu`和`active`两个类才会起作用

**CSS**
```
.menu {
    margin:0 auto;
}
.menu.active {
    font-weight:bold;
}
```

**HTML**
```
<div class="menu active"></div>
```

不过**多类选择器**`.className1.className2`在 **IE6+**以上才支持，关于浏览器对CSS选择器的支持会下面的内容统一整理列出表格。

### id选择器`#id`
id选择器与上面的类选择器使用很相似，通过在HTML文档中添加ID名称，然后与样式中的`#id`相匹配，**不过两者的最大的区别在于**，ID选择器是一个页面中唯一的值，不可多次使用，而class选择器是可以多次复用的。

**CSS**
```
#menu{
    margin:0 auto;
}
```

**HTML**
```
<div id="menu"></div>
```

### 群组选择器`s1,s2,...,sN`
群组选择器在开发中也是很常用的，它用于将相同样式的元素分组在一起，然后用逗号进行分割。

**CSS**
```
a:active,a:hover {
  outline: 0;
}
```

▲ 这里统一去掉了`a`链接在点击和浮动时的虚线焦点框。

### 后代选择器`E F`
后代选择器是**最常使用的选择器**之一，它也被称作包含选择器，用于匹配所有被`E`元素包含的`F`元素，这里`F`元素不管是`E`元素的子元素或者是孙元素或者是更深层次的关系，都将被选中。

**CSS**
```
.menu li{
    padding:0 ;
}
```

**HTML**
```
<ul id="menu">
    <li>
        <ul>
            <li></li>
        </ul>
    </li>
</ul>
```

▲ 这里`.menu`下的`li`元素和嵌套的`ul`元素下的`li`的元素都会被选择，进行清楚内边距。

### 子元素选择器`E > F`
子元素选择器只能选择某元素的子元素，这里的`F`元素仅仅是`E`元素的子元素才可以被选中

**CSS**
```
.menu > li{
    padding:0 ;
}
```

**HTML**
```
<ul id="menu">
    <li>
        <ul>
            <li></li>
        </ul>
    </li>
</ul>
```

▲ 将会对`.menu`下的`li`子元素选中，但会忽视内部嵌套的`li`元素

### 相邻兄弟元素选择器`E + F`
相邻兄弟选择器可以选择紧接在另一元素后的元素，但是他们必须有一个相同的父元素。比如`E`元素和`F`元素具有一个相同的父元素，而且`F`元素在`E`元素后面，这样我们就可以使用相邻兄弟元素选择器来选择`F`元素。

**CSS**
```
h1 + p {
    margin-top:5px;
}
```

**HTML**
```
<div>
    <h1>标题</h1>
    <p>内容</p>
</div>
```

▲ 将会选择`h1`元素后面的兄弟元素`p`


### 通用兄弟选择器`E ~ F`
通用兄弟元素选择器是**CSS3**新增加一种选择器，用于选择某元素后面的所有兄弟元素。它和相邻兄弟元素选择器用法相似，但不同于前者只是选择相邻的后一个元素，而通用兄弟元素选择器是选择**所有元素**。

**CSS**
```
h1 ~ p {
    margin-top:5px;
}
```

**HTML**
```
<div>
    <h1>标题</h1>
    <p>内容</p>
    <p>内容</p>
    <p>内容</p>
</div>
```
▲ 将会选择`h1`元素后面的所有的兄弟元素`p`





## 属性选择器
<table>
    <thead>
        <tr>
            <th>选择器</th>
            <th>描述</th>
            <th>CSS版本</th>
        </tr>
    </thead>
<tbody>
<tr>
<td>E[attr]</td>
  <td>匹配所有具有attr属性的E元素</td>
  <td>2.1</td>
</tr>
<tr>
<td>E[attr=value]</td>
  <td>匹配所有attr属性等于“value”的E元素</td>
  <td>2.1</td>
</tr>
<tr>
<td>E[attr~=value]</td>
  <td>匹配所有attr属性具有多个空格分隔的值、其中一个值等于“value”的E元素</td>
  <td>2.1</td>
</tr>
<tr>
<td>E[attr^=value]</td>
  <td>匹配所有attr属性值是以val开头的E元素</td>
  <td>2.1</td>
</tr>
<tr>
<td>E[attr$=value]</td>
  <td>匹配所有attr属性值是以val结束的E元素</td>
  <td>3</td>
</tr>
<tr>
<td>E[attr*=value]</td>
  <td>匹配所有attr属性值包含有“value”的E元素</td>
  <td>3</td>
</tr>
</tbody>
</table>

### E[attr]
`E[attr]`属性选择器是CSS3属性选择器最简单的一种，用于选择具有`att`属性的`E`元素。

**CSS**
```
img[alt] {
	margin: 10px;
}
```

**HTML**
```
<img src="url" alt="" />
<img src="url" />
```

▲ 将会选择到第一张图片，因为匹配到了alt属性，你也可以使用多属性的方式选择元素

```
img[src][alt] {
	margin: 10px;
}
```

### E[attr=value]
`E[attr="value"]`是指定了属性值`value`，从而缩小了范围可以更为精确的查找到自己想要的元素。

**CSS**
```
input[type="text"] {
	border: 2px solid #000;
}
```

**HTML**
```
<input type="text" />
<input type="submit" />
```

▲ 将会选择到`type="text"`表单元素。

### E[attr~=value]
如果你要根据属性值中的词列表的某个词来进行选择元素，那么就需要使用这种属性选择器：`E[attr~="value"]`，你会发现它和`E[attr="value"]`极为的相似，但是两者的区别是，属性选择器中有波浪（`~`）时属性值有`value`时就相匹配，没有波浪（`~`）时属性值要完全是`value`时才匹配。

**CSS**
```
div[class~="a"] {
	border: 2px solid #000;
}
```

**HTML**
```
<div class="a">1</div>
<div class="b">2</div>
<div class="a b">3</div>
```

▲ 将会选择到第1、3个`div`元素，因为匹配到了`class`属性，且属性值中有一个值为`a`

### E[attr^=value]
E[attr^="value"]属性选择器，指的是选择`attr`属性值以`“value”`开头的所有元素

**CSS**
```
div[class^="a"] {
	border: 2px solid #000;
}
```

**HTML**
```
<div class="abc">1</div>
<div class="acb">2</div>
<div class="bac">3</div>
```

▲ 将会选择到第1、2个`div`元素，因为匹配到了`class`属性，且属性值以`a`开头

### E[attr$=value]
`E[attr$="value"]`属性选择器刚好与`E[attr^="value"]`选择器相反，这里是选择`attr`属性值以"value"结尾的所有元素。

**CSS**
```
div[class$="c"] {
	border: 2px solid #000;
}
```

**HTML**
```
<div class="abc">1</div>
<div class="acb">2</div>
<div class="bac">3</div>
```

▲ 将会选择到第1、3个`div`元素，因为匹配到了`class`属性，且属性值以`c`结尾

### E[attr*=value]
`E[attr*="value"]`属性选择器表示的是选择`attr`属性值中包含`"value"`字符串的所有元素。

**CSS**
```
div[class*="b"] {
	border: 2px solid #000;
}
```

**HTML**
```
<div class="abc">1</div>
<div class="acb">2</div>
<div class="bac">3</div>
```

▲ 将会选择到所有的元素，因为匹配到了`class`属性，且属性值都包含了`b`

### E[attr|="val"] 
`E[attr|="val"]`是属性选择器中的最后一种，它被称作为特定属性选择器，这个选择器会选择`attr`属性值等于`value`或以`value-`开头的所有元素。

**CSS**
```
div[class|="a"] {
	border: 2px solid #000;
}
```

**HTML**
```
<div class="a-test">1</div>
<div class="b-test">2</div>
<div class="c-test">3</div>
```

▲  将会选择第1个`div`元素，因为匹配到了`class`属性，且属性值以紧跟着`"a-"`的开头

## 伪类选择器
### 动态伪类
一般动态伪类是在用户操作体验时触发的，最常见的就是超链接，它拥有访问前，鼠标悬停，被点击，已访问4种伪类效果。

* `E:link` 设置超链接a在未被访问前的样式
* `E:visited` 设置超链接a已被访问过时的样式
* `E:hover` 设置元素在其鼠标悬停时的样式
* `E:active` 设置元素在被用户激活时的样式

不过在使用时的时候，一定要注意书写的顺序，不然在不同的浏览器中会带来一些意想不到的错误。

```
a:link {}
a:visited {}
a:hover {}
a:active {}
```

最可靠的记忆顺序就是遵循爱恨原则：**l**(link)**ov**(visited)**e** **h**(hover)**a**(active)**te**, 即用喜欢(**love**)和讨厌(**hate**)两个词来概括。

还有一个用户行为的动态伪类`:focus`，常用于表单元素（触发onfocus事件发生）时的样式。

```
input[type="text"]:focus{
	border: 2px solid #000;
}
```

▲ 当用户聚焦到输入框内，会给输入框添加一个边框颜色。



### 表单状态伪类
我们把以下3种状态称作表单状态伪类，你会发现这些关键字就是HTML表单元素的属性，`checked`用于`type="radio"`和`type="checkbox"`够选中状态，`disabled`用于`type="text"`禁用的状态，而`enabled`这里表示`type="text"`可用的状态。

* `E:checked` 匹配用户界面上处于**选中**状态的元素E
* `E:enabled` 匹配用户界面上处于**可用**状态的元素E
* `E:disabled` 匹配用户界面上处于**禁用**状态的元素E

**CSS**
```
input[type="text"]:enabled {
	background: #fff;
}
input[type="text"]:disabled{
	background: #eee;
}
input:checked + span {
	background: red;
}
```

**HTML**
```
<input type="text" value="可用状态" />
<input type="text" value="可用状态" />
<input type="text" value="禁用状态" disabled="disabled" />
<input type="text" value="禁用状态" disabled="disabled" />
<label><input type="radio" name="radio" /><span>黑色</span></label>
```

▲ 将会给可用状态的文本框设置为白色(`#fff`)背景，禁用状态设置为灰色(`#eee`)背景，如果你选中了`radio`，它兄弟元素`span`的文本会变成红色


###结构伪类

* `E:first-child` 匹配父元素的第一个子元素E
* `E:last-child` 匹配父元素的最后一个子元素E
* `E:nth-child(n)` 匹配父元素的第n个子元素E，假设该子元素不是E，则选择符无效
* `E:nth-last-child(n)` 匹配父元素的倒数第n个子元素E，假设该子元素不是E，则选择符无效
* `E:first-of-type` 匹配同类型中的第一个同级兄弟元素E
* `E:last-of-type` 匹配同类型中的最后一个同级兄弟元素E
* `E:nth-of-type(n)` 匹配同类型中的第n个同级兄弟元素E
* `E:nth-last-of-type(n)` 匹配同类型中的倒数第n个同级兄弟元素E
* `E:only-child` 匹配父元素仅有的一个子元素E
* `E:only-of-type` 匹配同类型中的唯一的一个同级兄弟元素E
* `E:empty` 匹配没有任何子元素（包括text节点）的元素E


**E:first-child 和 E:last-child**
`E:first-child`是用来选择父元素的第一个子元素E，但是它必须为父元素的第一个子元素，不然会失效，举例说明 

**CSS**
```
p:first-child {
    color:red;
}
```

**HTML**
```
<div>
    <h1>标题</h1>
	<p>段落</p>
</div>
```

▲ 你会发现`p`元素的字体并没有变为红色，因为`p`元素前面还有个`h1`，它并不是父元素下的第一个子元素。

```
<div>
	<p>段落</p>
</div>
```

▲ 这时需要改变结构，效果才会正常。

而`E:last-child`与`E:first-child`选择器的作用类似，不同的是`E:last-child`选择是的元素的最后一个子元素。

**CSS**
```
p:last-child {
    color:red;
}
```

**HTML**
```
<div>
    <h1>标题</h1>
	<p>段落</p>
</div>
```

▲ 将`p`元素的字体设置为红色


**E:nth-child(n) 和 E:nth-last-child(n)**
`E:nth-child(n)`用于匹配父元素的第n个子元素E，假设该子元素不是E，则选择符无效。
该选择符允许使用一个乘法因子(n)来作为换算方式，如下: 

```
li:nth-child(2) { background:#fff}
```
▲ 选择第几个标签，“2可以是你想要的数字，最小从0开始”

```
li:nth-child(n+4) { background:#fff}
```
▲ 选择大于等于4标签，“n”表示从整数

```
li:nth-child(-n+4) { background:#fff}
```
▲ 选择小于等于4标签

```
li:nth-child(2n) { background:#fff}
li:nth-child(even) { background:#fff}
```
▲ 选择偶数标签，2n也可以是even

```
li:nth-child(2n-1) { background:#fff}
li:nth-child(odd) { background:#fff}
```
▲ 选择奇数标签，2n-1也可以是odd

```
li:nth-child(3n+1) { background:#fff}
```
▲ 自定义选择标签，3n+1表示“隔二取一”


而`E:nth-last-child(n)`又要开始反着来了，CSS3选择器有正就有反

```
li:nth-last-child(3) { background:#fff}
```
▲ 选择倒数第3个标签

**`E:first-of-type` 和 `E:last-of-type`**
`E:first-of-type`的使用方法类似于我们上面讲过的`E:first-child`,不过区别在于该选择器只会选择同类型的第一个元素，而不是父元素的第一个元素，举例说明：

**CSS**
```
p:first-of-type {
    color:red;
}
p:last-of-type {
    color:green;
}
```

**HTML**
```
<div>
    <h1>标题</h1>
	<p>段落</p>
    <p>段落</p>
    <div></div>
</div>
```

▲ 你会发现第一个`p`元素的字体被设置为红色，第二个`p`元素的字体被设置为绿色，这就是`E:first-of-type`和`E:first-child`不同之处。


**`E:nth-of-type(n)` 和 `E:nth-last-of-type(n)`**
这两个选择器的用法类似于`:nth-child(n)`和`E:nth-last-child(n)`，关于区别也是选择器只会选择同类型的兄弟元素，举个栗子
```
<div>
	<p>第1个p</p>
	<p>第2个p</p>
	<span>第1个span</span>
	<p>第3个p</p>
	<span>第2个span</span>
	<p>第4个p</p>
	<p>第5个p</p>
</div>
```

```
p:nth-child(3) {
    color:red;
}
```

▲ 如果使用`:nth-child(3)`你会发现第3个`p`元素文本并没有变成红色。就像我们之前说的，如果第n个子元素不是E，则是无效选择符，但n会递增。

```
p:nth-of-type(3) {
    color:red;
}
```

▲ 但是使用`:nth-of-type(3)`后会发现第3个`p`元素文本被设置为红色。


**`E:only-child` 和 `E:only-of-type`**
`E:only-child`用来匹配父元素仅有的一个子元素E，而`E:only-of-type`是表示一个元素它有很多个子元素，但是只会匹配其中只有一个子元素的元素，说起来有点绕口，来个栗子

**HTML**
```
<div>
	<p>段落</p>
</div>
<div>
	<div>容器</div>
	<p>段落</p>
	<div>容器</div>
</div>
```

```
p:only-child {
	color: red;
}
```
▲ 将会对第1个`div`元素下的`p`元素文本设置成红色。

```
p:only-of-type {
	color: red;
}
```
▲ 不仅会第1个`div`元素下的`p`元素文本设置成红色，也会对第2个`div`元素下的`p`元素文本设置成红色，因为它是p元素中唯一的一个同级兄弟元素。

<iframe width="100%" height="300" src="//jsfiddle.net/Alsiso/15h4ozee/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

**`E:empty`**
`E:empty`是用来选择没有任何内容的元素，包括text节点，也就是意味着连一个空格都不能有

**HTML**
```
<div>
	<p> </p>
	<p></p>
</div>
```

**CSS**
```
p:empty {
	height: 100px;
}
```
▲ 将会对第2个空元素`p`设置一个高度，为什么第一个会失效呢，因为该容器里面有一个空格。

### 否定类
`E:not(s)`用于匹配不含有s选择符的元素E，说起来不好理解，那么说一个最常用的开发场景，假如我们要对`ul`元素下的所有`li`都加上一个下边框用于内容分割，但是最后一个不需要，如下：

**HTML**
```
<ul>
	<li>列表1</li>
	<li>列表2</li>
    <li>列表3</li>
    <li>列表4</li>
</ul>
```

**CSS**
```
ul li:not(:last-child) {
	border-bottom: 1px solid #ddd;
}
```
▲ 将会对列表中除最后一项外的所有列表项添加一条下边框

## 伪元素选择器

* `E:first-letter` 选择文本块的第一个字母
* `E:first-line` 选择元素的第一行
* `E:before` 在元素前面插入内容，配合"content"使用
* `E:after` 在元素后面插入内容，配合"content"使用

以上四个伪元素选择器在CSS2.1都已经被支持，但在CSS3中将伪元素选择符前面的单个冒号(:)修改为双冒号(::)，如`E::first-letter`、`E::first-line`、`E::before`、`E::after`，不过之前的单冒号写法也是有效的。


###E::first-letter 和 E::first-line

```
p::first-letter {
    font-weight:bold;    
}
```
▲ 将会对文本块的第一个字母进行加粗


```
p::first-line {
    font-weight:bold;    
}
```

▲ 将会对段落的第一行文本进行加粗

###E::before 和 E::after
`E::before`和`E::after`是用来给元素的前面和后面差入内容，配合"content"使用，但它必须有值才能生效。

**HTML**
```
<div>me</div>
```

**CSS**
```
div:before{
    content:'you before'; 
    color:red;
}
div:after{
    content:'you after'; 
    color:green;
}
```

▲ 将会在`div`容器中的文本`me`加上添加后的内容并设置其颜色

###E::placeholder和 E::selection

* `E::placeholder` 选择文本块的第一个字母
* `E::selection` 选择文本块的第一个字母

`E::placeholder`用于设置对象文字占位符的样式，但是每个浏览器的CSS选择器都有所差异，需要针对每个浏览器做单独的设定，举个例子看代码

```
::-webkit-input-placeholder { /* WebKit browsers */
    color:    #999;
}
:-moz-placeholder { /* Mozilla Firefox 4 to 18 */
    color:    #999;
}
::-moz-placeholder { /* Mozilla Firefox 19+ */
    color:    #999;
}
:-ms-input-placeholder { /* Internet Explorer 10+ */
    color:    #999;
}
```

`E::selection`用于设置文本被选择时的样式，被定义的样式属性有3个，而且使用时需要对火狐浏览器单独设置。

```
p::-moz-selection{
    background:#000;
    color:#f00;
    text-shadow:1px 1px rgba(0,0,0,.3);
}
p::selection{
    background:#000;
    color:#f00;
    text-shadow:1px 1px rgba(0,0,0,.3);
}
```

## 第四代选择器
### 发展历史

自从**哈坤·利**提出CSS建议到1996年CSS1.0问世，距离今天已经有20个年头。
不过CSS的发展一直在持续，1997年组织了专门管CSS的工作组，并在1998年发布了CSS2.0，之后发布了修订版本的CSS2.1。

**CSS2.1** 是我们一直再用的，也是浏览器支持较为完整的一个版本。

CSS3 的开发工作早在2001年以前就启动了，不过发展到今天，大多数的现代浏览器对CSS3属性和选择器支持良好，除了一些微软IE浏览器的较老版本。

历史前进的步伐并不会停止的，新的CSS4也正由W3C编辑团队研发中。在CSS4中引进了许多的新变化，不过基本选择器是不会有变化的，更多的还是添加一些伪类，那么接下来一起看看增加的内容。

提醒：**目前这些代码功能可能还在实验规范阶段，浏览器并没有得到支持，所以并不能投入使用** ！

### 升级内容

**否定类** `E:not(s,s,s..)` 
`E:not`其实在选择器已经出现在CSS3了，它用于匹配不含有s选择符的元素E，上面我们讲过它的使用方法，但是它只能用于简单选择器，伪类，标签，id，类和类选择器参数。不过在CSS4中得到了升级，具体区别

```
p:not(.header) { 
    font-weight: normal; 
}  
```

▲ **CSS3**将会对除了`.header`类以外的文本加粗

```
p:not(.header, .footer) { 
    font-weight: normal; 
}  
```

▲ **CSS4**通过传入一个用逗号，将会对除了`.header`和`.footer`类以外的文本加粗

**关联类** `E:has(s)` 
这个选择器通过一个参数（选择符），去匹配与某一元素对应的任意选择器，举个例子

```
a:has(>img) {  
    border: 1px solid #000; 
}  
```

▲ 将会对所有带有`img`元素的`a`元素加个黑色的边框

**匹配任何伪类`E:matches`**
这个伪类选择器可以规则运用在所有的选择器组中，它能帮我们简写多组选择器的规则，例子说明，

```
<section>
    <h1>标题</h1>
</section>
<nav>
    <h1>标题</h1>
</nav>
```

▲ 上面的两个容器都有一个`h1标题元素，如何对容器下的`h1`字体进行字体颜色设置呢

```
section h1,nav h1{
    color:red;
}

:matches(section, nav) h1 {
    color: red;
}
```

▲ 这一种是传统的方法，第二种就是`:matches`方法。

**位置伪类`E:local-link`和`E:local-link(n)`** 

位置伪类是访问者在你网站上的位置

* `:local-link(0)` 代表一个超连接元素，其target和文档的URL是在同一个源中。 
* `:local-link(1)` 代表一个超连接元素，其target和文档的URL是在同一个源中。
* `:local-link(2)` 代表一个超连接元素，其target和文档的URL是在同一个源中。

```
/* 将会匹配 http://example.com/ link(s) */
:local-link(0) {
    color: red;
}
 
/* 将会匹配 http://example.com/year/ link(s) */
:local-link(1) {
    color: red;
}
 
/* 将会匹配 http://example.com/year/month/ link(s) */
:local-link(2) {
    color: red;
}
```


**表单状态伪类 `E:indeterminate`** 
`checkbox`中的`indeterminate`属性用于展示半选择状态，这个属性只是改变`checkbox`的外观，不对它的`checked`属性产生影响，CSS4选择器中也增加了半选择状态的伪类。

```
:indeterminate {
    opacity: 0.6;
}
```

**表单状态伪类 `E:required`**和 `E:optional`
`required`属性是HTML5新添加的，用于规定必需在提交之前填写输入字段

```
:required {
    border: 1px solid red;
}
:optional {
    border: 1px solid gray;
}
```

```
<input type="text" required="required" />
<input type="text" />
```

▲ 第一个设置了`required`属性的表单元素将会设置一个红色边框，而第二个没有设置该属性的，将会设置一个灰色边框。


**范围限制伪类`E:in-range`和`E:out-of-range`**
用于表单字段值范围的限制，取决于表单的`min`和`max`属性

```
:in-range {
    background-color:green;
}
 
:out-of-range {
    background-color:red;
}
```

```
<input type="number" value="5" max="10" min="1"  />
```

▲ 如果你输入的值在设置的最小和最大值范围内，那么表单背景会呈现为绿色，如果超出了限制，那么会呈现为红色。

关于更多的CSS4选择器，可参考这里的 [示例介绍][6]。


  [1]: http://segmentfault.com/u/alsiso/questions
  [2]: https://github.com/Alsiso/everyday
  [3]: http://segmentfault.com/a/1190000003021766
  [4]: http://shawphy.com/2010/09/no-css-reset.html
  [5]: http://segmentfault.com/q/1010000002997970
  [6]: http://css4-selectors.com/selectors/