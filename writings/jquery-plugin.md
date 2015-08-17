基于jQuery插件的方式编写代码
----

### 声明方法
在开始编写jQuery插件时，我们有必要了解一下插件的基本结构，所有的jQuery插件都声明为jQuery.fn对象的方法：

```
jQuery.fn.blockButton = function () {
      //code here
};
```

### 使用方法

```
$("#btn").blockButton();
```
### 匿名函数
在上个声明方法中我并没有使用$，这是为了避免命名冲突，如果要用 $ 的话，可以像下面这样把插件代码封装在一个自执行的匿名函数中，然后传入参数jQuery

```
(function($){
    $.fn.blockButton = function () {
        //code here
    };
})(jQUery);
```

### 接收多个参数

```
(function($){
	$.fn.blockButton = function(options) {    //经常用options表示有多个参数。
	    var defaults = {
	        'color': 'red',
	        'background': 'blue'
	    };
	    var settings = $.extend(defaults, options);
	    return this.css({
	        'color': settings.color,
	        'settings': settings.background
	    });
	}
})(jQUery);
```
调用时，字体颜色可以自定义，背景颜色会运用插件里的默认值：

```
$('btn').blockButton({
    'color': 'yellow'
});
```
