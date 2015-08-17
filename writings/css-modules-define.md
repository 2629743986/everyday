CSS 模块化命名规范
----

### 命名规范
#### 模块名
统一采用横杠`ui-a`作为连接符，不可使用下划线`ui_a`，或者驼峰标识`uiA`
尽量让人看到名字就能知道是什么模块，比如 ui-tab， ui-nav 这样的命名：

```
.ui-tab{}
```

#### 模块整体状态 = 模块名 + 状态
常用状态有：hover, current, selected, disabled, focus, blur, checked, success, error 等

```
.ui-tab{}
.ui-tab-current{}
```
#### 子模块 = 模块名 + 子模块名
常用模块名有：cnt(content)，hd(header)，text(txt)，img(images/pic)，title，item，cell 等， 只要词义表达了组件要实现的功能或者要表现出来的的外观就可以了。

```
.ui-tab{}
.ui-tab-current{}
.ui-tab-cnt {}
```

#### 子模块状态 = 模块名 + 子模块名 + 状态

```
.ui-tab{}
.ui-tab-current{}
.ui-tab-cnt {}
.ui-tab-cnt-error {}
```

### 完整的例子

```
.ui-tab {}
.ui-tab ul {}
.ui-tab li {}
.ui-tab-items {}
.ui-tab-item a {}
.ui-tab-item-current a {}
```

```
<div class="ui-tab">
    <ul class="ui-tab-items">
        <li class="ui-tab-item ui-tab-item-current">
            <a href="javascript:;">全部交易</a>
        </li>
        <li class="ui-tab-item">
            <a href="javascript:;">进行中的交易</a>
        </li>
        <li class="ui-tab-item">
            <a href="javascript:;">等待发货的交易</a>
        </li>
        <li class="ui-tab-item">
            <a href="javascript:;">未确认收获的交易</a>
        </li>
    </ul>
</div>
```

### 常用的CSS命名
#### (1)页面结构
- 容器: container
- 页头：header
- 内容：content/container
- 页面主体：main
- 页尾：footer
- 导航：nav
- 侧栏：sidebar
- 栏目：column
- 页面外围控制整体佈局宽度：wrapper
- 左右中：left right center
#### (2)导航
- 导航：nav
- 主导航：mainnav
- 子导航：subnav
- 顶导航：topnav
- 边导航：sidebar
- 左导航：leftsidebar
- 右导航：rightsidebar
- 菜单：menu
- 子菜单：submenu
- 标题: title
- 摘要: summary
#### (3)功能
- 标志：logo
- 广告：banner
- 登陆：login
- 登录条：loginbar
- 注册：register
- 搜索：search
- 功能区：shop
- 标题：title
- 加入：joinus
- 状态：status
- 按钮：btn
- 滚动：scroll
- 标签页：tab
- 文章列表：list
- 提示信息：msg
- 当前的: current
- 小技巧：tips
- 图标: icon
- 注释：note
- 指南：guild
- 服务：service
- 热点：hot
- 新闻：news
- 下载：download
- 投票：vote
- 合作伙伴：partner
- 友情链接：link
- 版权：copyright
