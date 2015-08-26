## 前言
之前整理了CSS选择器的基础使用，这一节首先会罗列出选择器被浏览器支持的情况，然后对选择器常见的一些问题，还有一些实用技巧，以及性能优化相关的建议。

## 浏览器支持

### 不支持 IE6 

以下选择器不支持**IE6**，只支持 **IE6+** 的浏览器

#### 基本选择器

<table>
    <thead>
        <tr>
            <th>选择器</th>
            <th>描述</th>
            <th>版本</th>
        </tr>
    </thead>
<tbody>
<tr>
<td>s1,s2,...,sN</td>
  <td>群组选择器，同时匹配所有s1元素或s2元素</td>
  <td>2.1</td>
</tr>
<tr>
<td>E > F</td>
  <td>子元素选择器，匹配所有E元素的子元素F</td>
  <td>2.1</td>
</tr>
<tr>
<td>E + F</td>
  <td>毗邻元素选择器，匹配所有紧随E元素之后的同级元素F</td>
  <td>2.1</td>
</tr>
<tr>
<td>E ~ F</td>
  <td>匹配任何E标签之后的同级F标签</td>
  <td>3</td>
</tr>
</tbody>
</table>

#### 属性选择器

<table>
    <thead>
        <tr>
            <th>选择器</th>
            <th>描述</th>
            <th>版本</th>
        </tr>
    </thead>
<tbody>
<tr>
<td>E[attr]</td>
  <td>匹配att属性的E元素</td>
  <td>2.1</td>
</tr>
<tr>
<td>E[attr="val"]</td>
  <td>匹配att属性且属性值等于val的E元素</td>
  <td>2.1</td>
</tr>
<tr>
<td>E[attr~="val"]</td>
  <td>匹配att属性且属性值中的词列表有一个等于val的E元素</td>
  <td>2.1</td>
</tr>
<tr>
<td>E[attr^="val"]</td>
  <td>匹配att属性且属性值为以val开头的字符串的E元素</td>
  <td>3</td>
</tr>
<tr>
<td>E[attr$="val"]</td>
  <td>匹配att属性且属性值为以val结尾的字符串的E元素</td>
  <td>3</td>
</tr>
<tr>
<td>E[attr*="val"]</td>
  <td>匹配att属性且属性值为包含val的字符串的E元素</td>
  <td>3</td>
</tr>
<tr>
<td>E[att|="val"]</td>
  <td>匹配att属性且属性值为以val开头并用连接符"-"分隔的字符串的E元素</td>
  <td>2.1</td>
</tr>
</tbody>
</table>

#### 伪类选择器

<table>
    <thead>
        <tr>
            <th>选择器</th>
            <th>描述</th>
            <th>版本</th>
        </tr>
    </thead>
<tbody>
<tr>
<td>E:hover</td>
  <td>设置元素在其鼠标悬停时的样式</td>
  <td>2.1</td>
</tr>
<tr>
<td>E:first-child</td>
  <td>匹配父元素的第一个子元素E</td>
  <td>2.1</td>
</tr>
</tbody>
</table>

`E:hover`在IE6中只有a元素可用

#### 伪元素选择器

<table>
    <thead>
        <tr>
            <th>选择器</th>
            <th>描述</th>
            <th>版本</th>
        </tr>
    </thead>
<tbody>
<tr>
<td>E:first-letter</td>
  <td>选择文本块的第一个字母</td>
  <td>2.1</td>
</tr>
<tr>
<td>E:first-line</td>
  <td>选择元素的第一行</td>
  <td>2.1</td>
</tr>
</tbody>
</table>



### （IE7+）不支持 IE6 / 7

以下选择器不支持**IE6，IE7**，只支持 **IE7+** 的浏览器

#### 伪类选择器

<table>
    <thead>
        <tr>
            <th>选择器</th>
            <th>描述</th>
            <th>版本</th>
        </tr>
    </thead>
<tbody>
<tr>
<td>E:focus</td>
  <td>设置对象在成为输入焦点时的样式</td>
  <td>2.1</td>
</tr>
</tbody>
</table>

#### 伪元素选择器

<table>
    <thead>
        <tr>
            <th>选择器</th>
            <th>描述</th>
            <th>版本</th>
        </tr>
    </thead>
<tbody>
<tr>
<td>E:before</td>
  <td>在元素前面插入内容，配合"content"使用</td>
  <td>2.1</td>
</tr>
<tr>
<td>E:after</td>
  <td>在元素后面插入内容，配合"content"使用</td>
  <td>2.1</td>
</tr>
</tbody>
</table>

### 不支持 IE6 / 7 / 8

以下选择器不支持**IE6，IE7，IE8**，只支持 **IE8+** 的浏览器

#### 伪类选择器

<table>
    <thead>
        <tr>
            <th>选择器</th>
            <th>描述</th>
            <th>版本</th>
        </tr>
    </thead>
<tbody>
<tr>
<td>E:checked</td>
  <td>匹配用户界面上处于选中状态的元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:enabled</td>
  <td>匹配用户界面上处于可用状态的元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:disabled</td>
  <td>匹配用户界面上处于禁用状态的元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:root</td>
  <td>匹配文档的根元素，对于HTML文档，就是HTML元素</td>
  <td>3</td>
</tr>
<tr>
<td>E:last-child</td>
  <td>匹配父元素的最后一个子元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:nth-last-child(n)</td>
  <td>匹配父元素的倒数第n个子元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:nth-of-type(n)</td>
  <td>匹配同类型中的第n个同级兄弟元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:nth-last-of-type(n)</td>
  <td>匹配同类型中的倒数第n个同级兄弟元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:first-of-type</td>
  <td>匹配同类型中的第一个同级兄弟元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:last-of-type</td>
  <td>匹配同类型中的最后一个同级兄弟元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:only-child</td>
  <td>匹配父元素仅有的一个子元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:only-of-type</td>
  <td>匹配同类型中的唯一的一个同级兄弟元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:empty</td>
  <td>匹配没有任何子元素（包括text节点）的元素E</td>
  <td>3</td>
</tr>
<tr>
<td>E:not(s)</td>
  <td>匹配不含有s选择符的元素</td>
  <td>3</td>
</tr>
<tr>
<td>E:target</td>
  <td>匹配文档中特定"id"点击后的效果</td>
  <td>3</td>
</tr>
</tbody>
</table>

#### 伪元素选择器

<table>
    <thead>
        <tr>
            <th>选择器</th>
            <th>描述</th>
            <th>版本</th>
        </tr>
    </thead>
<tbody>
<tr>
<td>E::first-letter</td>
  <td>选择文本块的第一个字母</td>
  <td>3</td>
</tr>
<tr>
<td>E::first-line</td>
  <td>选择元素的第一行</td>
  <td>3</td>
</tr>
<tr>
<td>E::before</td>
  <td>在元素前面插入内容，配合"content"使用</td>
  <td>3</td>
</tr>
<tr>
<td>E::after</td>
  <td>在元素后面插入内容，配合"content"使用</td>
  <td>3</td>
</tr>
<tr>
<td>E::selection</td>
  <td>设置对象被选择时的样式</td>
  <td>3</td>
</tr>
<tr>
</tbody>
</table>


### 让IE6-8支持伪类和属性选择器

如何才能让IE6~8支持CSS3伪类和属性选择器，也许你已经想到了，我们会用JavaScript工具来进行辅助，那么刚好[`selectivizr`][1]就可以完成这件事情，而且使用起来很简单，只要把`selectivizr.js`引入到页面上就可以了，如下：

```
<!- -[if (gte IE 6)&(lte IE 8)]>

      <script type="text/javascript" src="selectivizr.js"></script>

<![endif]- ->
```

但是使用它还有一些注意事项：

1. 必须要引用一个JavaScript库，比如jQuery
2. 只能解析`<link>`标签引入的样式，如果是`<style>`定义的样式是不会解析的
3. 动态生成的DOM不会做二次映射
4. 需要在标准模式的DTD才能够生效

项目地址：http://selectivizr.com

## 常见问题与Bug

### `*` 通配符造成继承失效

```
* {
    color:red;
}

#test{
    color:blue; 
}
```

```
<div id='test'>
    <a href="#">text</a>
</div>
```
▲ 最终text的颜色却是红色的

按照我们的理解，`id`的优先级是高于`*`通配符的，而文字也本应该继承`id`元素的color值，所以最终的文字应该是蓝色呀。

所以这里混淆了一个概念，继承的样式的优先级永远低于元素本身的样式，包括通配符选择器，所以大家在开发中，应该尽可能的避免滥用通配符，以免带来一些隐性问题。

关于这个问题，还可以参考《[关于CSS特殊性的问题][2]》

而在IE6及更早浏览器并不支持通配选择符(`*`)，只是将它忽略了，所以也变相的能看到效果。

### E:hover 失效

`E:hover`伪类用于设置元素在其鼠标悬停时的样式，但是在某种情况会导致效果失效，如下:

```
#test {
    background:red;
}
#test div { 
    display:none;
}
#test:hover div{
    display:block;
    background:yellow;
}
```

```
<div id="test">触发我<div>看到我了吧</div></div>
```

▲ 当触发`#test:hover`时，此效果是在**IE6**中是无效的，因为在IE6中，`E:hover`伪类仅能用于a（超链接）对象，且该`a`对象必须要拥有`href`属性。

`E:hover`还有一种失效的状态，是大家最常见的，代码如下：
```
a:link {color:gray;}
a:hover{color:green;}
a:visited{color:yellow;}
a:active{color:blue;}
```

```
<a href="#nogo">文字</a>
```

▲ 当超链接处于`a:hover`时，你会发现其效果是无效，文字的颜色不会变成绿色，这是因为超链接的伪类样式书写是有固定顺序的，不能颠倒，这四个属性正确的定义顺序为：
```
a:link {}
a:visited {}
a:hover {}
a:active {}
```

###E:focus 失效

```

#test:focus + p {
    font-weight:bold;
}
```

```
<button id="test">点击我触发focus</button>
<p>文字</p>
```

▲ 当点击`button`按钮触发`:focus`时将邻近元素的文字进行加粗，但是这个效果在**IE8**是失效的，如何来修复它呢，只需要添加一个空的`:focus`选择器，如下：

```
#test:focus + p {
    font-weight:bold;
}
#test:focus {}
```

### E:first-line 失效

如果在当前选择器内使用了`!important`，`:first-line`伪类内部的定义的属性会被完全忽略，示例：

```
p {
    color:blue;
}
p:first-line {
    color:red !important;
}
```

```
<p>第一行文字，<br/>第二行文字</p>
```
▲ 正常情况下第一行的文字会变成红色，但是在IE8浏览器却忽略它没有任何变化，如何来解决这个问题呢，把`!important`去掉就好了，如下：。

```
p {
    color:blue;
}
p:first-line {
    color:red;
}
```

### E:first-letter 失效

`E:first-letter`失效和`E:first-line`失效的问题是相同的，解决方案请参考上方。



### E > F 失效
就是子选择器中间有注释会导致属性失效，如下：

```
#test > 
/*子选择器*/
p {
	color:red;
}
```

```
<div id="test">
    <p>文字</p>
</div>
```

▲  如果你非要这样写注释，那么在IE7下会导致子选择器失效，同样，`E + F`邻近选择器也有同样的问题，如何解决呢，不在选择器中间添加注释就可以了。


## 性能优化

CSS 选择器我们都在使用，但是如何让它变的更简洁，高效呢？ 
首先选择器对性能的影响源于**浏览器匹配选择器和文档元素时所消耗的时间**，所以优化选择器的原则是应尽量避免使用消耗更多匹配时间的选择器，但是在此之前我们需要先了解浏览器的匹配机制，就是它是如何读取我们的选择器的。

### 选择器匹配机制

```
#nav > a {
    color:red;
}
```

当我们看到这个选择器的时候，会认为首先会找到id为`nav`的元素，然后在找到其子元素，将样式属性应用到`a`元素上。

事实上，却恰恰相反，因为浏览器读取选择器时，不是按照我们的阅读习惯从左到右，而是遵循的**从选择器的右边到左边进行读取的**。

当我们知道这个匹配机制后，再回来看这个选择器，浏览器必须先遍历页面中所有的 a 元素，然后查找其父元素的`id`是否为`nav`，这样一来你就会发看似高效的选择器在实际中的匹配开销是很高的。


理解了CSS选择器从右到左匹配的机制后，我们再看以下两种选择器：

```
div #nav
```

```
#nav div
```

你是否会认为第2种选择器的效率要高于第1种，那么就错了，其实第一个选择器的效率更高，因为第一个选择器的**关键选择器**使用了`#id`选择器”，而第二个选择器的**关键选择器**使用的是`div`标签选择器。

这里所说的**关键选择器**，就是CSS选择器中最右边部分，它是被浏览器最先寻找的，那么哪类选择器是最高效的？哪个是会影响选择器效率的关键选择器？



### 选择器效率

在上面内容中我们了解浏览器的匹配机制，以及关键选择器的重要性，那么哪些CSS选择器能够减少性能损耗呢？

Google 资深web开发工程师 [Steve Souders][3] 对 CSS 选择器的执行效率从高到低做了一个排序：

 1. id选择器（#id）
 2. 类选择器（.className）
 3. 标签选择器（div,h1,p）
 4. 相邻选择器（h1+p）
 5. 子选择器（ul > li）
 6. 后代选择器（li a）
 7. 通配符选择器（*）
 8. 属性选择器（a[rel="external"]）
 9. 伪类选择器（a:hover,li:nth-child）




从Steve Souders的`CSS Test`我们可以看出`#id`选择器和`.className`类选择器在速度上的差异很小很小。而在一个`a`标签选择器的测试上显示，它比`#id`选择器和类选择器的速度慢了很多，从这里我们可以看出`#id`、`.className`选择器 和 `a`标签、`li a`后代选择器中间的差异较大，但是相互之间的差异较小。

接下来举几个示例：

```
#nav {}
.menu{}
```
```
p#nav {}
p.menu {}
```

▲ 上面的选择器效率要高于下面的选择器，标签元素会降低选择器效率

### 优化建议

我们理解了CSS选择器从右到左匹配的机制，也了解关键选择器的重要性，以及CSS选择器的效率排序，那么在使用选择器的时候，通过避免不恰当的使用，来提升 CSS 选择器性能。

#### 避免使用通用选择器

```
#nav * {…}
```

▲ 这个选择器所做的是选择所有在页面上的单个元素（是每个单个的元素），然后去看看它们是否有一个`#nav`的父元素。这是非常不高效选择器，开销太大了，应该避免关键选择器是通配选择器的情况。

#### 避免使用标签或 class 选择器限制 id 选择器

```
/* Bad */
div#nav {…}
.menuBalck#menu {…}

/* Good */
#nav {…}
#menu {…}
```

▲ ID选择器本身就是唯一的，加上div反而增加不必要的匹配；

#### 避免使用标签限制 class 选择器

```
/* Bad */
span.red {…}

/* Good */
.text-red {…}
```

▲ 在标签上定义`class`选择器，在开发和维护时容易混淆，一般不建议这样写。

#### 避免使用多层标签选择器。使用 class 选择器替换，减少css查找

```
/* Bad */
a[href="#"] > span > em {…}

/* Good */
.className {}
```

▲ 这种情况建议直接定义.className 选择器，然后使用`<em class="className"></em>`


#### 避免过渡使用子选择器
```
/* Bad */
div ul li a {}
div > ul > li > a {}

/* Good */
.className {…}
```

▲ 这种情况建议直接定义.className 选择器，然后使用`<a class="className"></a>`

#### 避免过度限制选择器

```
/* Bad */
html body .wrapper #content a {}

/* Good */
#content a {}
```

▲ 这里至少有3个选择器是完全不需要的，过度限制选择器使浏览器工作比它实际需要的更繁重，花费的时间更多，所以这里应该避免。

#### 利用可继承性
```
/* Bad */
#nav > li > a { color:red; } 

/* Good */
#nav { color:red; }
```

▲ 在使用选择器之前，请先考虑利用继承性实现



  [1]: http://selectivizr.com/
  [2]: http://segmentfault.com/a/1190000000453851
  [3]: http://stevesouders.com/