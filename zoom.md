## 缩放

为了使用缩放功能，你最好使用`iscroll-zoom.js`脚本。

### <small>options.</small>zoom

此属性设置为`true`启用缩放功能。

默认值：`false`

### <small>options.</small>zoomMax

最大缩放级数。

默认值：`4`

### <small>options.</small>zoomMin

最小缩放级数。

默认值：`1`

### <small>options.</small>zoomStart

初始的缩放级数。

默认值：`1`

### <small>options.</small>wheelAction

鼠标滚轮的动作可以设置为`'zoom'`，这样在滚动滚轮时缩放操作会代替原来的滚动操作。

默认值：`undefined`（即：鼠标滚轮滚动）

和前面的示例一样，一个好的缩放功能的配置如下：

```js
myScroll = new IScroll('#wrapper', {
    zoom: true,
    mouseWheel: true,
    wheelAction: 'zoom'
});
```

> 缩放功能使用的CSS的转换功能。iScroll只能在支持此CSS功能的浏览器上执行。

> 一些浏览器（特别是基于webkit的）采取的快照缩放区域就放在硬件合成层(比如当你申请转换)。该快照作为纹理的缩放区域,它几乎不能被更新。这意味着您的纹理将基于 **scale 1** 进行缩放,将导致文本和图像模糊,清晰度低。

> 一个简单的解决方案是使用实际分辨率双倍（或者三倍）装载内容，然后 放到一个按照`scale(0.5)`比例缩小的div中。这种方法大多数情况下能适用。

请参考 [缩放示例](http://lab.cubiq.org/iscroll5/demos/zoom/)。

### zoom(scale, x, y, time)

一个有意思的的方法，能让你进行缩放编程。

`scale`是缩放因子。

`x` 和 `y`是缩放关注点，即缩放的中心。如果没有指定，这个中心就是屏幕中心。

`time` is the duration of the animation in milliseconds (optional).
`time`是毫秒级别的动画周期（可选项）。
