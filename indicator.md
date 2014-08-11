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

请参考[迷你地图示例](http://lab.cubiq.org/iscroll5/demos/minimap/)，你将体验`indicators`选项的神奇力量。

你应该已经注意到选项`indicators`是复数，是的，实际上，传递一个对象数组你可以得到一个虚拟的无限大小的指示器。我不知道你是否需要，但是，这里我是想你介绍参数设置，所以要提及此。

## <span id="parallax-scrolling">视差滚动</span>

视差滚动是[指示器](#indicators)功能的一个 *附属功能*

指示器是一个遵循主滚动条移动和动画的层。如果你了解它你就会理解这个功能背后的力量。增加这个功能你就可以创建任意数量的指示器和视差滚动。


请参考 [视差滚动示例](http://lab.cubiq.org/iscroll5/demos/parallax/).

## 滚动的编程接口

当然还可以通过编程来进行滚动。

### scrollTo(x, y, time, easing)

对应存在的一个叫做`myScroll`的iScroll实例，可以通过下面的方式滚动到任意的位置：

```js
myScroll.scrollTo(0, -100);
```

通过上面的方式将向下滚动100个像素。记住：0永远是左上角。需要滚动你必须传递负数。

`time` 和 `easing`是可选项。他们控制滚动周期（毫秒级别）和动画的擦除效果。

擦除功能是一个有效的`IScroll.utils.ease`对象。例如应用一个一秒的经典擦除动画你应该这么做：

```js
    myScroll.scrollTo(0, -100, 1000, IScroll.utils.ease.elastic);
```

擦除动画的类型选项有：`quadratic`, `circular`, `back`, `bounce`, `elastic`。

### scrollBy(x, y, time, easing)

和上面一个方法类似，但是可以传递X和Y的值从当前位置进行滚动。

```js
myScroll.scrollBy(0, -10);
```

上面这个语句将在当前位置向下滚动10个像素。如果你当前所在位置为-100，那么滚动结束后位置为-110.

### scrollToElement(el, time, offsetX, offsetY, easing)

这是一个很有用的方法，你会喜欢它的。

在这个方法中只有一个强制的参数就是`el`。传递一个元素或者一个选择器，iScroll将尝试滚动到这个元素的左上角位置。

`time`是可选项，用于设置动画周期。

`offsetX` 和 `offsetY`定义像素级的偏移量，所以你可以滚动到元素并且加上特别的偏移量。但并不仅限于此。如果把这两个参数设置为`true`，元素将会位于屏幕的中间。请参考例子 [滚动到元素](http://lab.cubiq.org/iscroll5/demos/scroll-to-element/) example。

`easing`参数和**scrollTo**方法里的一样。
