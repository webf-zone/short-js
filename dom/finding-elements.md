Finding Elements

Front-end world before jQuery was completely a different ballgame. Finding any DOM element within HTML page was cumbersome. You had only three options:

```js
// Find DOM element with `id`
document.getElementById(id: string)

// Find list of DOM elements with `tag`
document.getElementsByTagName(tagName: string)

// Find list of DOM elements having class `className`
document.getElementsByClassName(className: string)
```

Imagine, if you are asked to: **Change colors of all paragraphs \(`p` tag\) who are children of `div` element having class `highlight`**. Solving such simple problem was pain. You would do following:

1. Find all `div `elements using `getElementsByTagName`.
2. Loop them and filter all `div` having class `highlight`.
3. For each **div **found, get its children using `divElement.children`.
4. Then change the color.

Doing this with CSS is probably easy:

```css
div.highlight p {
    color: yello;
}
```

Back then, people wished if there could be a way as simple as using CSS selector. Enter jQuery and world changed for better. This  cumbersome four step process reduced to single line:

```js
jQuery('div.highlight p').css('color', 'yellow');
```



