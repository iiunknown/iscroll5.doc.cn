
## 对齐

iScroll能对齐到固定的位置和元素。

### <small>options.</small>snap

最简单的对齐配置如下：

```js
var myScroll = new IScroll('#wrapper', {
    snap: true
});
```
这将按照页面容器的大小自动分割滚动条。

`snap`属性也可以传递字符类型类型的值。这个值是滚动条将要对齐到的元素的选择器。比如下面：
```js
var myScroll = new IScroll('#wrapper', {
    snap: 'li'
});
```
这个示例中滚动条将会对齐到每一个`LI`标记的元素。

下面将帮助你快速浏览iScroll提供的关于对齐的一系列有趣的方法。


### goToPage(x, y, time, easing)

`x` 和 `y`呈现你想滚动到横向轴或者纵向轴的页面数。如果你需要在单个唯独上使用滚动条，只需要为你不需要的轴向传递`0`值。

`time`属性是动画周期，`easing`属性是滚动到指定点使用的擦除功能类型。请参考[高级功能](#advanced-features)中的**option.bounceEasing**。这两个属性都是可选项。

```js
myScroll.goToPage(10, 0, 1000);
```

上面这个例子将在一秒内沿着横向滚动到第10页。

### next()<br/>prev()

滚动到当前位置的下一页或者前一页。
