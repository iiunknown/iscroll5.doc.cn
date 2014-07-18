
<h2 id="refresh">Mastering the refresh method</h2>

iScroll needs to know the exact dimensions of both the wrapper and the scroller. They are computed at start up but if your elements change in size, we need to tell iScroll that you are messing with the DOM.

This is achieved by calling the `refresh` method with the right timing. Please follow me closely, understanding this will save you hours of frustration.

Every time you touch the DOM the browser renderer repaints the page. Once this repaint has happened we can safely read the new DOM properties. The repaint phase is not instantaneous and it happens only at the end of the scope that triggered it. That's why we need to give the renderer a little rest before refreshing the iScroll.

To ensure that javascript gets the updated properties you should defer the refreh with something like this:

    ajax('page.php', onCompletion);

    function onCompletion () {
        // Update here your DOM

        setTimeout(function () {
            myScroll.refresh();
        }, 0);
    };

We have placed the `refresh()` call into a zero timeout. That is likely all you need to correctly refresh the iScroll boundaries. There are other ways to wait for the repaint, but the zero-timeout has proven pretty solid.

<div class="tip">
<p>Consider that if you have a very complex HTML structure you may give the browser some more rest and raise the timeout to 100 or 200 milliseconds.</p>

<p>This is generally true for all the tasks that have to be done on the DOM. Always give the renderer some rest.</p>
</div>

<h2 id="custom-events">Custom events</h2>

iScroll also emits some useful custom events you can hook to.

To register them you use the `on(type, fn)` method.

    myScroll = new IScroll('#wrapper');
    myScroll.on('scrollEnd', doSomething);

The above code executes the `doSomething` function every time the content stops scrolling.

The available types are:

* **beforeScrollStart**, executed as soon as user touches the screen but before the scrolling has initiated.
* **scrollCancel**, scroll initiated but didn't happen.
* **scrollStart**, the scroll started.
* **scroll**, the content is scrolling. Available only in `scroll-probe.js` edition. See [onScroll event](#onscroll).
* **scrollEnd**, content stopped scrolling.
* **flick**, user flicked left/right.
* **zoomStart**, user started zooming.
* **zoomEnd**, zoom ended.

<h2 id="onscroll">onScroll event</h2>

The `scroll` event is available on **iScroll probe edition** only (`iscroll-probe.js`). The probe behavior can be altered through the `probeType` option.

### <small>options.</small>probeType

This regulates the probe aggressiveness or the frequency at which the `scroll` event is fired. Valid values are: `1`, `2`, `3`. The higher the number the more aggressive the probe. The more aggressive the probe the higher the impact on the CPU.

`probeType: 1` has no impact on performance. The `scroll` event is fired only when the scroller is not busy doing its stuff.

`probeType: 2` always executes the `scroll` event except during momentum and bounce. This resembles the native `onScroll` event.

`probeType: 3` emits the `scroll` event with a to-the-pixel precision. Note that the scrolling is forced to `requestAnimationFrame` (ie: `useTransition:false`).

Please see the [probe demo](http://lab.cubiq.org/iscroll5/demos/probe/).

<h2 id="key-bindings">Key bindings</h2>

You can activate support for keyboards and remote controls with the `keyBindings` option. By default iScroll listens to the arrow keys, page up/down, home/end but they are (wait for it) totally customizable.

You can pass an object with the list of key codes you want iScroll to react to.

The default values are as follow:

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

You can also pass a string (eg: `pageUp: 'a'`) and iScroll will convert it for you. You could just think of a key code and iScroll would read it out of your mind.

<h2 id="scroller-info">Useful scroller info</h2>

iScroll stores many useful information that you can use to augment your application.

You will probably find useful:

* **myScroll.x/y**, current position
* **myScroll.directionX/Y**, last direction (-1 down/right, 0 still, 1 up/left)
* **myScroll.currentPage**, current snap point info

These pieces of information may be useful when dealing with custom events. Eg:

    myScroll = new IScroll('#wrapper');
    myScroll.on('scrollEnd', function () {
        if ( this.x < -1000 ) {
            // do something
        }
    });

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
