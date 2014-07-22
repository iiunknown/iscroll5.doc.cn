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

This regulates the probe aggressiveness or the frequency at which the `scroll` event is fired. Valid values are: `1`, `2`, `3`. The higher the number the more aggressive the probe. The more aggressive the probe the higher the impact on the CPU.

`probeType: 1` has no impact on performance. The `scroll` event is fired only when the scroller is not busy doing its stuff.

`probeType: 2` always executes the `scroll` event except during momentum and bounce. This resembles the native `onScroll` event.

`probeType: 3` emits the `scroll` event with a to-the-pixel precision. Note that the scrolling is forced to `requestAnimationFrame` (ie: `useTransition:false`).

Please see the [probe demo](http://lab.cubiq.org/iscroll5/demos/probe/).

