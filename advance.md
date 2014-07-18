## 高级选项

下面这些选项主要针对核心开发人员。

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
