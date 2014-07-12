
<h2 id="snap">Snap</h2>

iScroll can snap to fixed positions and elements.

### <small>options.</small>snap

The simplest snap config is as follow:

    var myScroll = new IScroll('#wrapper', {
        snap: true
    });

This would automatically split the scroller into pages the size of the container.

`snap` also takes a string as a value. The string will be the selector to the elements the scroller will be snapped to. So the following

    var myScroll = new IScroll('#wrapper', {
        snap: 'li'
    });

would snap to each and every `LI` tag.

To help you navigate through the snap points iScroll grants access to a series of interesting methods.

### goToPage(x, y, time, easing)

`x` and `y` represent the page number you want to scroll to in the horizontal or vertical axes (yeah, it's the plural of *axis*, I checked). If the scroller in mono-dimensional, just pass `0` to the axis you don't need.

`time` is the duration of the animation, `easing` the easing function used to scroll to the point. Refer to the **option.bounceEasing** in the [Advanced features](#advanced-features). They are both optional.

    myScroll.goToPage(10, 0, 1000);

This would scroll to the 10th page on the horizontal axis in 1 second.

### next()<br/>prev()

Go to the next and previous page based on current position.

<h2 id="zoom">Zoom</h2>

To use the pinch/zoom functionality you better use the `iscroll-zoom.js` script.

### <small>options.</small>zoom

Set this to `true` to activate zoom.

Default: `false`

### <small>options.</small>zoomMax

Maximum zoom level.

Default: `4`

### <small>options.</small>zoomMin

Minimum zoom level.

Default: `1`

### <small>options.</small>zoomStart

Starting zoom level.

Default: `1`

### <small>options.</small>wheelAction

Wheel action can be set to `'zoom'` to have the wheel regulate the zoom level instead of scrolling position.

Default: `undefined` (ie: the mouse wheel scrolls)

To sum up, a nice zoom config would be:

    myScroll = new IScroll('#wrapper', {
        zoom: true,
        mouseWheel: true,
        wheelAction: 'zoom'
    });

<div class="important">
<p>The zoom is performed with CSS transform. iScroll can zoom only on browsers that support that.</p>
</div>

<div class="tip">
<p>Some browsers (notably webkit based ones) take a snapshot of the zooming area as soon as they are placed on the hardware compositing layer (say as soon as you apply a transform to them). This snapshot is used as a texture for the zooming area and it can hardly be updated. This means that your texture will be based on elements at <strong>scale 1</strong> and zooming in will result in blurred, low definition text and images.</p>

<p>A simple solution is to load content at double (or triple) its actual resolution and scale it down inside a <code>scale(0.5)</code> div. This should be enough to grant you a better result. I hope to be able to post more demos soon</p>
</div>

Refer to the [zoom demo](http://lab.cubiq.org/iscroll5/demos/zoom/).

### zoom(scale, x, y, time)

Juicy method that lets you zoom programmatically.

`scale` is the zoom factor.

`x` and `y` the focus point, aka the center of the zoom. If not specified, the center of the screen will be used.

`time` is the duration of the animation in milliseconds (optional).

<h2 id="infinite-scrolling">Infinite scrolling</h2>

iScroll integrates a smart caching system that allows to handle of a virtually infinite amount of data using (and reusing) just a bunch of elements.

Infinite scrolling is in an early stage of development and although it can be considered stable, it is not ready for wide consumption.

Please review the [infinite demo](http://lab.cubiq.org/iscroll5/demos/infinite/) and send your suggestions and bug reports.

I will add more details as soon as the functionality evolves.

<h2 id="advanced-options">Advanced options</h2>

For the hardcore developer.

### <small>options.</small>bindToWrapper

The `move` event is normally bound to the document and not the scroll container. When you move the cursor/finger out of the wrapper the scrolling keeps going. This is usually what you want, but you can also bind the move event to wrapper itself. Doing so as soon as the pointer leaves the container the scroll stops.

Default: `false`

### <small>options.</small>bounceEasing

Easing function performed during the bounce animation. Valid values are: `'quadratic'`, `'circular'`, `'back'`, `'bounce'`, `'elastic'`. See the [bounce easing demo](http://lab.cubiq.org/iscroll5/demos/bounce-easing/), drag the scroller down and release.

`bounceEasing` is a bit smarter than that. You can also feed a custom easing function, like so:

    bounceEasing: {
        style: 'cubic-bezier(0,0,1,1)',
        fn: function (k) { return k; }
    }

The above would perform a linear easing. The `style` option is used every time the animation is executed with CSS transitions, `fn` is used with `requestAnimationFrame`. If the easing function is too complex and can't be represented by a cubic bezier just pass `''` (empty string) as `style`.

Note that `bounce` and `elastic` can't be performed by CSS transitions.

Default: `'circular'`

### <small>options.</small>bounceTime

Duration in millisecond of the bounce animation.

Default: `600`

### <small>options.</small>deceleration

This value can be altered to change the momentum animation duration/speed. Higher numbers make the animation shorter. Sensible results can be experienced starting with a value of `0.01`, bigger than that basically doesn't make any momentum at all.

Default: `0.0006`

### <small>options.</small>mouseWheelSpeed

Set the speed of the mouse wheel.

Default: `20`

### <small>options.</small>preventDefaultException

These are all the exceptions when `preventDefault()` would be fired anyway despite the **preventDefault** option value.

This is a pretty powerful option, if you don't want to `preventDefault()` on all elements with *formfield* class name for example, you could pass the following:

    preventDefaultException: { className: /(^|\s)formfield(\s|$)/ }

Default: `{ tagName: /^(INPUT|TEXTAREA|BUTTON|SELECT)$/ }`.

### <small>options.</small>resizePolling

When you resize the window iScroll has to recalculate elements position and dimension. This might be a pretty daunting task for the poor little fella. To give it some rest the polling is set to 60 milliseconds.

By reducing this value you get better visual effect but the script becomes more aggressive on the CPU. The default value seems a good compromise.

Default: `60`

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
