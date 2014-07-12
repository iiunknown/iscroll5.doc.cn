## 指示器

上面所有关于滚动条的选项实际上是包装了一个底层的选项`indicators`。它看起来或多或少像这样：
```js
var myScroll = new IScroll('#wrapper', {
    indicators: {
        el: [element|element selector]
        fade: false,
        ignoreBoundaries: false,
        interactive: false,
        listenX: true,
        listenY: true,
        resize: true,
        shrink: false,
        speedRatioX: 0,
        speedRatioY: 0,
    }
});
```
### <small>options.indicators.</small>el

这是一个强制性的参数，它保留了指向滚动条容器元素的引用。容器里的第一个子元素就是指示器。注意，滚动条可以在你的文档的任意地方，它不需要在滚动条包装器内。你是不是开始感到这样一个工具的厉害？

有效的语法如下：
```js
indicators: {
    el: document.getElementById('indicator')
}
```

更简单的方式：
```js
indicators: {
    el: '#indicator'
}
```
### <small>options.indicators.</small>ignoreBoundaries

这个属性是告诉指示器忽略它容器所带来的边界。当我们能改变滚动条速度的比率，在让滚动条滚动时这个属性很有用。比如你想让指示器是滚动条速度的两倍，指示器将很快到达它的结尾。这个属性被用在[视差滚动](#parallax-scrolling)。

默认值：`false`

### <small>options.indicators.</small>listenX<br/><small>options.indicators.</small>listenY

指示器的那一个轴（横向和纵向）被侦听。可以设置一个或者都设置

默认值：`true`

### <small>options.indicators.</small>speedRatioX<br/><small>options.indicators.</small>speedRatioY

指示器移动的速度和主要滚动条大小的关系。默认情况下是设置为自动。你很少需要去改变这个值。

默认值：`0`

### <small>options.indicators.</small>fade<br/><small>options.indicators.</small>interactive<br/><small>options.indicators.</small>resize</br><small>options.indicators.</small>shrink

这几个选项和我们已经介绍过的[滚动条](#scrollbars)中的一样，在这里不重复介绍。

<div class="important">
<p><strong>Do not cross the streams. It would be bad!</strong> Do not mix the scrollbars syntax (<code>options.scrollbars</code>, <code>options.fadeScrollbars</code>, <code>options.interactiveScrollbars</code>, ...) with the indicators! Use one or the other.</p>
</div>
<div class="important">
<p><strong>Do not cross the streams. It would be bad!</strong> Do not mix the scrollbars syntax (<code>options.scrollbars</code>, <code>options.fadeScrollbars</code>, <code>options.interactiveScrollbars</code>, ...) with the indicators! Use one or the other.</p>
</div>

Have a look at the [minimap demo](http://lab.cubiq.org/iscroll5/demos/minimap/) to get a glance at the power of the `indicators` option.
请参考[迷你地图示例](http://lab.cubiq.org/iscroll5/demos/minimap/)，你将看到`indicators`选项的神奇力量。

The wittiest of you would have noticed that `indicators` is actually plural... Yes, exactly, passing an array of objects you can have a virtually infinite number of indicators. I don't know what you may need them for, but hey! who am I to argue about your scrollbar preferences?
你应该已经注意到选项`indicators`是复数，是的，实际上，传递一个对象数组你可以得到一个虚拟的无限大小的指示器。我不知道你是否需要，但是，这里我是想你介绍参数设置，所以要提及此。

## <span id="parallax-scrolling">Parallax scrolling</span>
## <span id="parallax-scrolling">视差滚动</span>

Parallax scrolling is just a *collateral damage* of the [Indicators](#indicators) functionality.

An indicator is just a layer that follows the movement and animation applied to the main scroller. If you see it like that you'll understand the power behind this feature. To this add that you can have any number of indicators and the parallax scrolling is served.

Please refer to the [parallax demo](http://lab.cubiq.org/iscroll5/demos/parallax/).

## Scrolling programmatically

You silly! Of course you can scroll programmaticaly!

### scrollTo(x, y, time, easing)

Say your iScroll instance resides into the `myScroll` variable. You can easily scroll to any position with the following syntax:

    myScroll.scrollTo(0, -100);

That would scroll down by 100 pixels. Remember: 0 is always the top left corner. To scroll you have to pass negative numbers.

`time` and `easing` are optional. They regulates the duration (in ms) and the easing function of the animation respectively.

The easing functions are available in the `IScroll.utils.ease` object. For example to apply a 1 second elastic easing you'd do:

    myScroll.scrollTo(0, -100, 1000, IScroll.utils.ease.elastic);

The available options are: `quadratic`, `circular`, `back`, `bounce`, `elastic`.

### scrollBy(x, y, time, easing)

Same as above but X and Y are relative to the current position.

    myScroll.scrollBy(0, -10);

Would scroll 10 pixels down. If you are at -100, you'll end up at -110.

### scrollToElement(el, time, offsetX, offsetY, easing)

You're gonna like this. Sit tight.

The only mandatory parameter is `el`. Pass an element or a selector and iScroll will try to scroll to the top/left of that element.

`time` is optional and sets the animation duration.

`offsetX` and `offsetY` define an offset in pixels, so that you can scroll to that element plus a the specified offset. Not only that. If you set them to `true` the element will be centered on screen. Refer to the [scroll to element](http://lab.cubiq.org/iscroll5/demos/scroll-to-element/) example.

`easing` works the same way as per the **scrollTo** method.
