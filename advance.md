## 高级选项

下面这些选项主要针对核心开发人员。

### <small>options.</small>bindToWrapper

`move`事件通常绑定到文档而不是滚动器容器（wrapper）。当你在滚动器容器（wrapper）外移动光标/手指，滚动条将不断滚动。这通常是你想要的,但是你也可以绑定事件转移到滚动器容器（wrapper）本身。这样做一旦指针离开了容器，滚动就会停止。

Default: `false`
默认值：`false`

### <small>options.</small>bounceEasing

擦除功能在弹跳动画过程中执行。有效的值为：`'quadratic'`, `'circular'`, `'back'`, `'bounce'`, `'elastic'`. 参见[bounce easing demo](http://lab.cubiq.org/iscroll5/demos/bounce-easing/)，往下拽滚动条然后释放。

`bounceEasing`比上面的示例更强大。你可以自定义一个消除的方式，比如：

```js
bounceEasing: {
    style: 'cubic-bezier(0,0,1,1)',
    fn: function (k) { return k; }
}
```

上面这个示例将执行一个线性的擦出。`style`选项将在在每次动画执行时使用CSS转场执行。`fn`和`requestAnimationFrame`一起使用。如果一个擦出功能太复杂，不能由一个三次贝塞尔曲线展现，那么为`style`属性传递 `''` （空字符串）。

注意：`bounce` 和 `elastic`这两种方式不能被CSS转场执行。

Default: `'circular'`
默认值：`'circular'`

### <small>options.</small>bounceTime

弹跳动画的持续时间，使用毫秒级。

默认值：`600`

### <small>options.</small>deceleration

这个值可以改变改变动画的势头持续时间/速度。更高的数字使动画更短。你可以从`0.01`开始去体验，这个值和基本的值比较，基本上没有动能。

默认值：`0.0006`

### <small>options.</small>mouseWheelSpeed

设置鼠标滚轮滚动的速度值。

默认值：`20`

### <small>options.</small>preventDefaultException

调用`preventDefault()`方法时所有的异常将被触发，尽管**preventDefault**设置了值。

这是一个强大的选项，如果你想为所有包含*formfield*样式名称的元素上应用`preventDefault()`方法，你可以设置为下面的值：
```js
preventDefaultException: { className: /(^|\s)formfield(\s|$)/ }
```

默认值：`{ tagName: /^(INPUT|TEXTAREA|BUTTON|SELECT)$/ }`.

### <small>options.</small>resizePolling

当你改变窗口的大小iScroll重新计算元素的位置和尺寸。这可能是一个相当艰巨的任务。轮询设置为60毫秒。

通过降低这个值你获得更好的视觉效果，但会占用更多的CPU资源。默认值是一个很好的折中。

默认值：`60`
