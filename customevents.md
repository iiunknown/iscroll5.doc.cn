## 自定义事件
<h2 id="custom-events">Custom events</h2>

iScroll还提供额一些你可以挂靠的有用的自定义事件。

使用`on(type, fn)`方法注册事件。
```js
myScroll = new IScroll('#wrapper');
myScroll.on('scrollEnd', doSomething);
```

上面的代码会在每次滚动停止是执行`doSomething`方法。

可以挂靠的事件如下：

* **beforeScrollStart**，在用户触摸屏幕但还没有开始滚动时触发。
* **scrollCancel**，滚动初始化完成，但没有执行。
* **scrollStart**，开始滚动
* **scroll**，内容滚动时触发，只有在`scroll-probe.js`版本中有效，请参考[onScroll event](#onscroll)。
* **scrollEnd**，停止滚动时触发。
* **flick**，用户打开左/右。
* **zoomStart**，开始缩放。
* **zoomEnd**，缩放结束。

## onScroll事件

The `scroll` event is available on **iScroll probe edition** only (`iscroll-probe.js`). The probe behavior can be altered through the `probeType` option.
`scroll`事件在**iScroll probe edition**版本中有效（仅包含在`iscroll-probe.js`脚本文件中）。可以通过改变`probeType`选项值来改变`scroll`事件的触发时机。

### <small>options.</small>probeType

这个属性是调节在`scroll`事件触发中探针的活跃度或者频率。有效值有：`1`, `2`, `3`。数值越高表示更活跃的探测。探针活跃度越高对CPU的影响就越大。

`probeType: 1` 对性能没有影响。`scroll`事件只有在滚动条不繁忙的时候触发。
`probeType: 2` 除了在势能和反弹范围内，将在`scroll`事件周期内一直执行。这类似于原生的`onScroll`事件。

`probeType: 3` 像素级的触发`scroll`事件。注意，此时滚动只关注`requestAnimationFrame` (即：`useTransition:false`).

请参考 [probe demo](http://lab.cubiq.org/iscroll5/demos/probe/).

