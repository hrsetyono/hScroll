# hScroll

A simple parallax scrolling using CSS variables. Only 3.6 KB gzipped.

**TABLE OF CONTENTS**

- [Demo](#demo)
- [Features](#features)
- [Function & Parameters](#function--parameters)
- [Example](#example)
- [Animation Timing](#animation-timing)
- [Tips](#tips)
- [Requirements](#requirements)
- [Credit](#credit)

## Demo

| Name | Link |
| --- | --- |
| Basic Implementation | [View in Codepen](https://codepen.io/hrsetyono/pen/MZRRqe) |
| Parallax Banner | [View in Codepen](https://codepen.io/hrsetyono/pen/EGzYBr) |

## Features

- **Smooth Performance** - We only modify CSS Variable as you scroll.
- **Lightweight** - Our script is only 3.6 KB gzipped.
- **No dependencies** - Just plain old JS.

## Function & Parameters

```
hScroll( targets, args )
```

`targets` (Node / NodeList) - Element used as threshold on when to start/stop animating

`args` (obj) - Possible arguments are:

- **from** (string) - When to start animating. Default: middle-bottom.

  The value `middle-bottom` means: When the middle of the element reaches the bottom viewport, start animating.

  You can mix-match these 3 keywords: `middle`, `top`, and `bottom`. For example `top-bottom` means start animating as soon as the element enters the viewport.
	
- **to** (string) - When to stop animating. Default: middle-top.

- **direct** (bool) - If true, CSS changes is applied to the element. If false, applied to `<body>`. Default: false.

- **--var-name** (string) - Set starting and ending value for the variable. Format: `A to B`.


## Example

You have an image that you want to add "Fade in" animation:

```html
<div class="my-image">
  <img src="...">
</div>
```

Use CSS Variable to set the properties you want to animate.

```css
.my-image {
  opacity: var( --opacity )
  transform: translateY( var( --tr-y ) );
}
```

Finally, use hScroll to animate that CSS variable.

```js
document.addEventListener('DOMContentLoaded', () => {

  hScroll( document.querySelector('.my-image'), {
    '--opacity': '0 to 1',
    '--tr-y': '50px to 0'
  } );

} );
```

## Animation Timing

The default animation timing is **linear**. So if the CSS value is `0 to 100px` and we already scrolled 30% from the starting position, our variable is now `30px`.

You can add custom timing by appending the value like below:

```js
hScroll( document.querySelector('.my-elem'), {
  '--opacity': '0 to 1 elasticInOut',
});
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

You can open `index3.html` from this repo to see the difference in speed.

## Tips

- By default, hScroll applies changes to `<body>`. Which mean you can reuse it across elements instead of creating more instances.

- Only animate `transform` and `opacity` property.

- Don't animate everything at once and don't animate too many properties. Browsers don't like this.

----

### Requirements

hScroll also depends on the following browser features and APIs:

- [CSS Custom Properties](https://drafts.csswg.org/css-variables/#defining-variables)
- [Object.assign](http://www.ecma-international.org/ecma-262/6.0/#sec-object.assign)
- [requestAnimationFrame](https://www.w3.org/TR/animation-timing/#dom-windowanimationtiming-requestanimationframe)

Some of these APIs are capable of being polyfilled in older browsers. Check the linked resources above to determine if you must polyfill to achieve your desired level of browser support.

### Credit

This is a fork of [basicScroll](https://github.com/electerious/basicScroll) with simpler implementation. So big thanks to [Tobias Reich](https://github.com/electerious) for creating an awesome basis for this library.