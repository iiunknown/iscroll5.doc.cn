##按键绑定

你可以激活`keyBindings`选项来支持键盘控制。默认情况下iScroll监听方向键，上下翻页建，home/end键，但这些按键绑定完全可以自定义。

你可以通过传递一个包含按键代码列表的对象来进行按键绑定。

默认的按键值如下:
```js
keyBindings: {
    pageUp: 33,
    pageDown: 34,
    end: 35,
    home: 36,
    left: 37,
    up: 38,
    right: 39,
    down: 40
}
```

当然你也可以传递字符串进行按键绑定（例如：`pageUp: 'a'`）。只要你设置了对于的按键值，那么iScroll就会响应你的设置。
