## 入门

你想成为iScroll大师。行，这就是我写以下内容的目的。

最好的学习iScroll的方法是看示例。在存档文件中你会发现一个叫做`demo`的文件夹[示例](https://github.com/cubiq/iscroll/tree/master/demos)。这里有大多数脚本功能的概述。

`IScroll`是一个类，每个需要使用滚动功能的区域均要进行初始化。每个页面上的iScroll实例数目在设备的CPU和内存能承受的范围内是没有限制的。

尽可能保持DOM结构的简洁。iScroll使用硬件合成层但是有一个限制硬件可以处理的元素。

最佳的HTML结构如下：
```html
<div id="wrapper">
    <ul>
        <li>...</li>
        <li>...</li>
        ...
    </ul>
</div>
```

iScroll作用于滚动区域的外层。在上面的例子中，`UL`元素能进行滚动。只有容器元素的第一个子元素能进行滚动，其他子元素完全被忽略。

`box-shadow`, `opacity`, `text-shadow` and alpha channels are all properties that don't go very well together with hardware acceleration. Scrolling might look good with few elements but as soon as your DOM becomes more complex you'll start experiencing lag and jerkiness.

Sometimes a background image to simulate the shadow performs better than `box-shadow`. The bottom line is: experiment with CSS properties, you'll be surprised by the difference in performance a small CSS change can do.

最基本的脚本初始化的方式如下：
```js
<script type="text/javascript">
var myScroll = new IScroll('#wrapper');
</script>
```

第一个参数可以是滚动容器元素的DOM选择器字符串，也可以是滚动容器元素的引用对象。下面是一个有效的语法：
```js
var wrapper = document.getElementById('wrapper');
var myScroll = new IScroll(wrapper);
```

所以基本上你要么直接传递元素，要么传递一个`querySelector`字符串。因此可以使用css名称代替ID去选择一个滚动器容器,如下:
```js
var myScroll = new IScroll('.wrapper');
```

注意，iScroll使用的是`querySelector` 而不是 `querySelectorAll`，所以iScroll只会作用到选择器选中元素的第一个。如果你需要对多个对象使用iScroll，你需要构建自己的循环机制。

<div class="tip">
<p>You don't strictly need to assign the instance to a variable (<code>myScroll</code>), but it is handy to keep a reference to the iScroll.</p>

<p>For example you could later check the <a href="#scroller-info">scroller position</a> or <a href="#destroy">unload unnecessary events</a> when you don't need the iScroll anymore.</p>
</div>
