移动端适配方案
----


### 视觉 UI
**产出物**

* 提供一套750px (iPhone6) 带有标注的视觉设计稿 
* 以及 750px * 2 的高清切图一套

**调整**

* 水平方向涉及到内容填充不做固定标注，如`winth:100px;`
* 水平方向涉及到内容填充只做间距与间隙的标注，`margin:0 10px;`

## 前端 FE

### 解决方案

* 将 viewport 设置为width=750
* 字体大小使用固定值px
* 垂直方向的高度和间距使用固定值px定值，
* 水平方向混合使用固定值`px`和百分比`%`或者弹性布局`flex`
* 图像元素根据容器情况，使用定值或者`background-size`缩放
* 动态设定`initial-scale`解决部分android中设定的viewport失效问题

**viewport**
```
<meta name="viewport" content="width=750,user-scalable=no">
```

**mobile-util.js**
该 JS 应在 head 中尽可能早的引入，减少重绘
```
<script type="text/javascript" src="js/mobile-util.js"></script>
```


