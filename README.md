# hScroll

A Simple Parallax scrolling using CSS variables. Only 3.6 KB gzipped.

> This is a jQuery wrapper for [basicScroll](https://github.com/electerious/basicScroll) with simpler implementation.

## Contents

- [Demos](#demos)
- [Setup](#setup)
- [Options](#options)
- [Animation Timing](#animation-timing)
- [Tips](#tips)
- [Requirements](#requirements)

## Demos

- [Basic Usage](https://codepen.io/hrsetyono/pen/MZRRqe)
- [Parallax Banner](https://codepen.io/hrsetyono/pen/EGzYBr)
- [More Demos from basicSlider](https://github.com/electerious/basicScroll#demos)


## Setup

1. Include the JS files before `</body>`. You can ignore the jQuery if you already added it. Also change the path to fit your project directory.

	```html
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
	<script src="js/h-scroll.min.js"></script>
	```

1. Create an element and set CSS variable in the property that you want to animate.

	```html
	<div class="my-elem">
	  <img src="...">
	</div>
	```

	```css
	.my-elem {
	  transform: rotate( var(--rotate) );
	  will-change: transform;
	  transition: transform .1 ease-in-out;
	}
	```

1. Apply hScroll to the element. Then set the starting and finishing value for the CSS variable.

	```js
	$(document).ready( function() {

	  $('.my-elem').hScroll({	
	    '--rotate': { from: 0, to: '180deg' }
	  });
		
	});
	```

1. **Done!** As simple as that.


## Options

Available options for hScroll are:

1. **from** - When to start animating. Default: middle-bottom.
1. **to** - When to stop animating. Default: middle-top.

	```js
	$('.my-elem').hScroll({
	  from: 'middle-bottom',
	  to: 'middle-top',
	  '--rotate': { from: 0, to: '180deg' }
	});
	```

	The value consists of 2 parts: First is the element, Second is the viewport. So `middle-bottom` means: When the middle of the element reached the bottom viewport.

	Possible values for both parts are: `top`, `middle`, and `bottom`.

1. **direct** - If true, apply the variable to the element directly. If false, applied to `<body>`. Default: false.

	If you inspect the element of the Demo, you will see that the variable changes is applied on `<body>`. This is intentional so you can reuse that variable when needed.


## Animation Timing

The default animation timing is **linear**. So if the CSS value is `0` to `100px` and we already scrolled 30% from the starting position, our variable is now `30px`.

By providing `timing` argument, we can modify the speed to suit your needs.

```js
$('.my-elem').hScroll({
  '--rotate': { from: 0, to: '180deg', timing: 'elasticInOut' }
});
```

Or add it as data attribute. But it will be applied to all CSS variables.

```html
<div class="my-elem" data-timing="elasticInOut">
  <img src="...">
</div>
```

Possible timing:

| Timing | | |
| --- | --- | --- |
| backInOut | backIn | backOut |
| bounceInOut | bounceIn | bounceOut |
| circInOut | circIn | circOut |
| cubicInOut | cubicIn | cubicOut |
| elasticInOut | elasticIn | elasticOut |
| expoInOut | expoIn | expoOut |
| quadInOut | quadIn | quadOut |
| quartInOut | quartIn | quartOut |
| quintInOut | quintIn | quintOut |
| sineInOut | sineIn | sineOut |
| linear | | |	


## Tips

- hScroll applies all [props](#props) globally by default. Try to reuse variables across elements instead of creating more instances.
- Only animate `transform` and `opacity` and use `will-change` to [hint browsers about the kind of changes](https://developer.mozilla.org/de/docs/Web/CSS/will-change). This way the browser can setup appropriate optimizations ahead of time before the element is actually changed.
- Don't animate everything at once and don't animate too many properties. Browsers don't like this.
- Smooth animations by adding a short transition to the element: `transform: translateY(var(--ty)); transition: transform .1s`.


## Requirements

hScroll depends on **jQuery**. Tested working on version 1.12.4.

hScroll also depends on the following browser features and APIs:

- [CSS Custom Properties](https://drafts.csswg.org/css-variables/#defining-variables)
- [Object.assign](http://www.ecma-international.org/ecma-262/6.0/#sec-object.assign)
- [requestAnimationFrame](https://www.w3.org/TR/animation-timing/#dom-windowanimationtiming-requestanimationframe)

Some of these APIs are capable of being polyfilled in older browsers. Check the linked resources above to determine if you must polyfill to achieve your desired level of browser support.