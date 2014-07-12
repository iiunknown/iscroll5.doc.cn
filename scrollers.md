## 滚动条

滚动条不只是像名字所表达的意义一样，在内部它们是作为*indicators*的引用。

一个指示器侦听滚动条的位置并且现实它在全局中的位置，但是它可以做更多的事情。

先从最基本的开始。

### <small>options.</small>scrollbars

正如我们在[基本功能介绍](#basic-features)中提到的，激活滚动条只需要做一件事情，这件事情就是：
```js
var myScroll = new IScroll('#wrapper', {
    scrollbars: true
});
```
当然这个默认的行为是可以定制的。

### <small>options.</small>fadeScrollbars
不想使用滚动条淡入淡出方式时，需要设置此属性为`false`以便节省资源。

默认值：`false`

### <small>options.</small>interactiveScrollbars
此属性可以让滚动条能拖动，用户可以与之交互。

默认值：`false`

### <small>options.</small>resizeScrollbars
滚动条尺寸改变基于容器和滚动区域的宽/高之间的比例。此属性设置为`false`让滚动条固定大小。这可能有助于自定义滚动条样式（[参考下面](#styling-the-scrollbar)）。

默认值：`true`

### <small>options.</small>shrinkScrollbars
当在滚动区域外面滚动时滚动条是否可以收缩到较小的尺寸。

有效的值为：`'clip'` 和 `'scale'`。

`'clip'`是移动指示器到它容器的外面，效果就是滚动条收缩起来，简单的移动到屏幕以外的区域。属性设置为此值后将大大的提升整个iScroll的性能。

值`'scale'`关闭属性`useTransition`，之后所有的动画效果将使用`requestAnimationFrame`实现。指示器实际上有各种尺寸，并且最终的效果最好。

默认值：`false`

注意改变大小不是在GPU上执行的，所以'scale' 是在CPU上执行。

如果你的应用程序将在多种设备上运行，我建议你使用选项`'scale'`，或者设置`'clip'` 为 `false` (例如：在较老的设备上应该设置为`'clip'` ，而在桌面浏览器上应设置为`'scale'`)。

请参考 [滚动条示例](http://lab.cubiq.org/iscroll5/demos/scrollbars/)。

<h3 id="styling-the-scrollbar">滚动条样式</h3>

如果你不喜欢默认的滚动条样式，而且你认为你可以做的更好，你可以自定义滚动条样式。第一步就是设置选项`scrollbars`的值为`'custom'`：
```js
var myScroll = new IScroll('#wrapper', {
    scrollbars: 'custom'
});
```

使用下面的CSS类可以简单的改变滚动条样式。

* **.iScrollHorizontalScrollbar**，这个样式应用到横向滚动条的容器。这个元素实际上承载了滚动条指示器。
* **.iScrollVerticalScrollbar**，和上面的样式类似，只不过适用于纵向滚动条容器。
* **.iScrollIndicator**，真正的滚动条指示器。
* **.iScrollBothScrollbars**，这个样式将在双向滚动条显示的情况下被加载到容器元素上。通常情况下其中一个（横向或者纵向）是可见的

[自定义滚动条样式示例](http://lab.cubiq.org/iscroll5/demos/styled-scrollbars/)。

如果你设置`resizeScrollbars: false`，滚动条将是固定大小，否则它将基于滚动区域的尺寸变化。

请接着阅读接下来的内容。
