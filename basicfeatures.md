## 基本功能

### <small>options.</small>bounce

当滚动器到达容器边界时他将执行一个小反弹动画。在老的或者性能低的设备上禁用反弹对实现平滑的滚动有帮助。

默认值：`true`

### <small>options.</small>click

为了重写原生滚动条，iScroll禁止了一些默认的浏览器行为，比如鼠标的点击。如果你想你的应用程序响应*click*事件，那么该设置次属性为`true`。请注意，建议使用自定义的`tap` 事件来代替它（见下面）。

默认属性：`false`

### <small>options.</small>disableMouse<br/><small>options.</small>disablePointer<br/><small>options.</small>disableTouch
默认情况下，iScroll监听所有的指针事件，并且对这些事件中第一个被触发的做出反应。这看上去是浪费资源，但是在大量的浏览器/设备上兼容，特定的事件侦测证明是无效的，所以*listen-to-all*是一个安全的做法。

如果你有一种设备侦测的内部机制，或者你知道你的脚本将在什么地方运行，你可以把你不需要的事件禁用（鼠标，指针或者触摸事件）。

下面的例子是禁用鼠标和指针事件：
```js
var myScroll = new IScroll('#wrapper', {
    disableMouse: true,
    disablePointer: true
});
```

默认值：`false`

### <small>options.</small>eventPassthrough

有些时候你想保留原生纵向的滚动条但想为横向滚动条增加iScroll功能（比如走马灯）。设置这个属性为`true`并且iScroll区域只将影响横向滚动，纵向滚动将滚动整个页面。

在移动设备上访问[event passthrough demo](http://lab.cubiq.org/iscroll5/demos/event-passthrough/)。注意，这个值也可以设置为`'horizontal'`，其作用和上面介绍的相反（横向滚动条保持原生，纵向滚动条使用iScroll）。

### <small>options.</small>freeScroll

此属性针对于两个两个纬度的滚动条（当你需要横向和纵向滚动条）。通常情况下你开始滚动一个方向上的滚动条，另外一个方向上会被锁定不动。有些时候，你需要无约束的移动（横向和纵向可以同时响应），在这样的情况下此属性需要设置为`true`。请参考 [2D scroll demo](http://lab.cubiq.org/iscroll5/demos/2d-scroll/)。

默认值：`false`

### <small>options.</small>keyBindings

此属性为`true`时激活键盘（和远程控制）绑定。请参考下面的[Key bindings](#key-bindings)内容。

默认值：`false`

### <small>options.</small>invertWheelDirection

当鼠标滚轮支持激活后，在有些情况下需要反转滚动的方向。（比如，鼠标滚轮向下滚动条向上，反之亦然）。

默认值：`false`

### <small>options.</small>momentum

在用户快速触摸屏幕时，你可以开/关势能动画。关闭此功能将大幅度提升性能。

默认值：`true`

### <small>options.</small>mouseWheel

侦听鼠标滚轮事件。

默认值：`false`

### <small>options.</small>preventDefault

当事件触发时师傅执行`preventDefault()`。此属性应该设置为`true`，除非你真的知道你需要怎么做。

请参考[Advanced features](#advanced-features)中的`preventDefaultException`，可以获取更多控制preventDefault行为的信息。

Default: `true`
默认值：`true`

### <small>options.</small>scrollbars

是否显示为默认的滚动条。更多信息请查看[Scrollbar](#scrollbar)

默认值：`false`

### <small>options.</small>scrollX<br/><small>options.</small>scrollY

默认情况下只有纵向滚动条可以使用。如果你需要使用横向滚动条，需要将`scrollX` 属性值设置为 `true`。请参考示例[horizontal demo](http://lab.cubiq.org/iscroll5/demos/horizontal/)。

也可以参考**freeScroll**选项。

默认值：`scrollX: false`，`scrollY: true`

注意属性 `scrollX/Y: true` 与`overflow: auto`有相同的效果。设置一个方向上的值为 `false` 可以节省一些检测的时间和CPU的计算周期。

### <small>options.</small>startX<br/><small>options.</small>startY

默认情况下iScroll从`0, 0` (top left)位置开始，通过此属性可以让滚动条从不同的位置开始滚动。

默认值：`0`

### <small>options.</small>tap

设置此属性为`true`，当滚动区域被点击或者触摸但并没有滚动时，可以让iScroll抛出一个自定义的`tap`事件。

这是处理与可以点击元素之间的用户交互的建议方式。侦听`tap`事件和侦听标准事件的方式一致。示例如下：
```js
element.addEventListener('tap', doSomething, false); \\ Native
$('#element').on('tap', doSomething); \\ jQuery
```

你可以通过传递一个字符串来自定义事件名称。比如：
```js
tap: 'myCustomTapEvent'
```

在这个示例里你应该侦听名为`myCustomTapEvent`的事件。

默认值：`false`
