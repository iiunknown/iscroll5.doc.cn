## 配置iScroll

在iScroll初始化阶段可以通过构造函数的第二个参数配置它。
```js
var myScroll = new IScroll('#wrapper', {
    mouseWheel: true,
    scrollbars: true
});
```

上面的例子示例了在iScroll初始化时开启鼠标滚轮支持和滚动条支持。

在初始化后你可以通过`options`对象访问*标准化*值。例如：
```js
console.dir(myScroll.options);
```

上面的语句将返回`myScroll`实例的配置信息。所谓的*标准化*意味着如果你设置`useTransform:true`，但是浏览器并不支持CSS transforms，那么`useTransform`属性值将为`false`。
