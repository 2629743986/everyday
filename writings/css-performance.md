CSS 性能优化
----

### 书写顺序

1.位置属性(position, top, right, z-index, display, float等)
2.大小(width, height, padding, margin)
3.文字系列(font, line-height, letter-spacing, color- text-align等)
4.背景(background, border等)
5.其他(animation, transition等)


```
/* Bad */
.example {
	color: red;
	z-index: -1;
	background-color: #9e0;
	display: inline-block;
	font-size: 14px;
}

/* Good */
.example {
	z-index: -1;
	display: inline-block;
	font-size: 14px;
	color: red;
	background-color: #9e0;
}

```

### 优化建议
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