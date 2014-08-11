##滚动条信息

iScroll存储了很多有用的信息，您可以使用它们来增强您的应用。

你可能会发现有用的：

* **myScroll.x/y**，当前位置
* **myScroll.directionX/Y**，最后的方向 (-1 down/right, 0 still, 1 up/left)
* **myScroll.currentPage**，当前对齐捕获点

下面是关于处理时间的代码示例：
```js
myScroll = new IScroll('#wrapper');
myScroll.on('scrollEnd', function () {
    if ( this.x < -1000 ) {
        // do something
    }
});
```

The above executes some code if the `x` position is lower than -1000px when the scroller stops. Note that I used `this` instead of `myScroll`, you can use both of course, but iScroll passes itself as `this` context when firing custom event functions.

<h2 id="destroy">Destroy</h2>

The public `destroy()` method can be used to free some memory when the iScroll is not needed anymore.

    myScroll.destroy();
    myScroll = null;

<h2 id="contributing">Contributing and CLA</h2>

If you want to contribute to the iScroll development, before I can accept your submission I have to ask you to sign the [Contributor License Agreement](http://cubiq.org/iscroll/cla/). Unfortunately that is the only way to enforce the openness of the script.

As an end user you have to do nothing of course. Actually the CLA ensures that nobody will even come after you asking for your first born for using the iScroll.

Please note that pull requests may take some time to be accepted. Testing iScroll is one of the most time consuming tasks of the project. iScroll works from desktop to smartphone, from tablets to smart TVs. I do not have physical access to all the testing devices, so before I can push a change I have to make sure that the new code is working everywhere.

Critical bugs are usually applied very quickly, but enhancements and coding style changes have to pass a longer review phase. *Remember that this is still a side project for me.*

<h2 id="whos">Who is using iScroll</h2>

It's impossible to track all the websites and applications that use the iScroll. It has been spotted on: Apple, Microsoft, People, LinkedIn, IKEA, Nike, Playboy, Bose, and countless others.

<h2 id="license">License (MIT)</h2>


Copyright (c) 2014 Matteo Spinelli, [cubiq.org](http://cubiq.org/)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
