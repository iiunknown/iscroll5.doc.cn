## 初始化

当DOM准备完成后iScroll需要被初始化。最保险的方式是在window的`onload`事件中启动它。在`DOMContentLoaded`事件中或者inline initialization中做也可以，需要记住的是脚本需要知道滚动区域的高度和宽度。如果你有一些图片在滚动区域导致不能立马获取区域的高度和宽度，iScroll的滚动尺寸有可能会错误。

为滚动起容器增加```position:relative```或者```absolute```样式。这将解决大多数滚动器容器大小计算不正确的问题。

综上所述，最小的iScroll配置如下：
```html
    <head>
    ...
    <script type="text/javascript" src="iscroll.js"></script>
    <script type="text/javascript">
    var myScroll;
    function loaded() {
        myScroll = new IScroll('#wrapper');
    }
    </script>
    </head>
    ...
    <body onload="loaded()">
    <div id="wrapper">
        <ul>
            <li>...</li>
            <li>...</li>
            ...
        </ul>
    </div>
    </body>
```

转到[barebone example](http://lab.cubiq.org/iscroll5/demos/barebone/)获取更多关于最小化 CSS/HTML结构的需求。

如果你有一个复杂的DOM结构，最好在<code>onload</code>事件之后适当的延迟，再去初始化iScroll。最好给浏览器100或者200毫秒的间隙再去初始化iScroll。
