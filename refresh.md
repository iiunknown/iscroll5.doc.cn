## 掌握刷新方法

iScroll需要知道包装器和滚动器确切的尺寸，在iScroll初始化的时候进行计算，如果元素大小发生了变化，需要告诉iScroll DOM发生了变化。

下面将提供调用`refresh`方法的正确时机。

每次触摸DOM，浏览器渲染器重绘页面。一旦发生了重画我们可以安全地读新的DOM属性。重新绘制阶段不是瞬时发生的只是范围结束时触发。这就是为什么我们需要给渲染器刷新iScroll之前一点时间。

为了确保javascript得到更新后的属性，应该像下面的例子这样使用刷新方法：
```js
ajax('page.php', onCompletion);

function onCompletion () {
    // Update here your DOM

    setTimeout(function () {
        myScroll.refresh();
    }, 0);
};
```

这里调用`refresh()`使用了零秒等待，如果你需要立即刷新iScroll边界就是如此使用。当然还有其他方法可以等待页面重绘，但零超时方式相当稳定。

> 如果你有一个相当复杂的HTML结构，你应该给浏览器更多的执行事件，可以设置100到200毫秒的超时时间。

> 这通常适用于所有任务必须在DOM上进行。通常给渲染器一些执行的时间。

