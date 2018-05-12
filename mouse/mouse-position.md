# Mouse Position

While building interactive web application, there is a need to get mouse position when certain event has happened. Commonly used mouse events are `click`, `mousemove`, etc. Ripple effects, animations, drap-n-drop, mouse position on canvas are the things where mouse position is frequently required.

Mouse position is a pair of x and y co-ordinate. x represents horizontal position whereas y stands for vertical position. But a simple search about mouse position will reveal that we have different values available namely, `clientY`, `pageY`, `screenY`, \`offsetY\`.

This short article is a simple attempt to illustrate the different positioning values.

## Understanding Mouse Event

Whenever user interacts with an application using a pointing device like a mouse or stylus, event object of type `MouseEvent` is generated for events like `click`, `mousedown`, `mouseup`, `mouseup`, `dblclick`.

All the positioning values are available on this object.

## Mouse Position Coordinates

Following diagram illustrates various y-positioning values:![](/assets/mouse-position.jpg)These values are best described as follows:

| Co-ordinates | Descriptions |
| :--- | :--- |
| PageY | Most useful value. PageY represents y-position of the mouse with respect to whole document. Any scrolling is also considered in the calculation of pageY. |
| ScreenY | Least useful value. It represent y-position with respect to actual physical screen/monitor. |
| ClientY | It represents y-position with respect to the viewport i.e. content area of the browser. Any scrolling is ignored in the calculation of the clientY. |

Of course, corresponding x-position values also exist but we will omit them here for the sake of simplification. Any arguments valid for y-position are equally applicable to x-position values.

### PageY

`pageY` is most used value as it considers the y-position of the mouse with respect to whole document. Using `pageX` and `pageY`, it becomes very easy to put absolutely positioned elements like context menus, tooltips, highligters, etc on web page. In reality, pageY is nothing but:

```js
pageY = clientY + document.body.scrollTop + document.documentElement.scrollTop;
```

During early days of browsers, `pageY` was not implemented across browsers and developers used above formula to calculate the `pageY` value.

### ScreenY

So far, I have not been really able to find any practical use of screenY value.

### ClientY

`clientY` is another useful value which is specially useful in dialog boxes and alike. It doesn't take scrolling into consideration. Clicking in the top-left corner of the client area will always result in a mouse event with a clientY value of 0, regardless of whether the page is scrolled vertically.

## Mouse Position in Canvas Element

HTML5 `Canvas` is graphics drawing API. It is useful for image composition, animations and games. In many cases, it is required to calculate `x` and `y` position of the mouse with respect to canvas `top-left` corner of the canvas. Using above properties on `MouseEvent`, it becomes very easy to calculate it:

```js
const canvas = document.getElementById('my-canvas');

canvas.addEventListener('click', (event) => {
    // x-position
    x = event.pageX - canvas.offsetLeft;

    // y-position
    y = event.pageY - canvas.offsetTop;
    
    const position = { x, y };
    
    // do something with position
    
}, false);
```

In fact, this technique is not just useful for canvas; it can be used with any element. In above example, using `offsetLeft` or `offsetTop` is not really foolproof. In real use, you should prefer to use `Element.getBoundingClientRect()`.

## OffsetX and OffsetY

As it turns out, there are two position values that can also be used - `event.offsetX` and `event.offsetY`.  But they are not used often due to earlier browser differences and incompatibility. Unlike name suggest, they don't return position of the mouse with respect to `offsetParent`. Rather, it does similar to what we were trying to do with the canvas example. `offsetX` and `offsetY` return co-ordinates of the mouse between the event and [padding edge of the target node](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/offsetY).

## MouseEvent x and y

Finally, you will also notice the presense of `x` and `y` properties on mouse event object. These properties are simply aliases for respective `clientX` and `clientY`.

