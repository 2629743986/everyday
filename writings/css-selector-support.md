## 浏览器支持
上一节讲选择器使用的时候，忘记了说明浏览器的支持情况了，在这里进行分类罗列一下，需要时可进行对照参考。

### 不支持 IE6 
### 基本选择器

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

### 不支持 IE6 / 7

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