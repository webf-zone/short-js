# Finding Elements

Front-end world before jQuery was completely a different ballgame. Finding any DOM element within HTML page was cumbersome. You had only three options:

```js
// Find DOM element with `id`
document.getElementById(id: string)

// Find list of DOM elements with `tag`
document.getElementsByTagName(tagName: string)

// Find list of DOM elements having class `className`
document.getElementsByClassName(className: string)
```

Imagine, if you are asked to: **Change colors of all paragraphs \(**`p`** tag\) who are children of **`div`** element having class **`highlight`. Solving such simple problem was pain. You would do following:

1. Find all `div`elements using `getElementsByTagName`.
2. Loop them and filter all `div` having class `highlight`.
3. For each **div **found, get its children using `divElement.children`.
4. Then change the color.

Doing this with CSS is probably easy:

```css
div.highlight p { color: yello; }
```

Back then, people wished if there could be a way as simple as using CSS selector. Enter jQuery and world changed for better. This  cumbersome four step process reduced to single line:

```js
jQuery('div.highlight p').css('color', 'yellow');
```

At that time, jQuery became de facto; it was used by more than 50% websites around the world. And as such, it is one of the classic question used in interview: **Change colors of all paragraphs who are children of div element having class highlight "using plain JavaScript"**. And I am still waiting for a person to come up with an answer.

## Selector API

jQuery left the big legacy behind and as such jQuery inspired **Selector API** is proof of that legacy. You can use **selector API** to do what jQuery is doing:

```js
// Returns first matching element that matches the specified selector
// Returns null if no matching element found
document.querySelector(cssSelector: string)

// Returns list of DOM nodes containing all elements that matches the selector
// Returns empty list if not elements are found
document.querySelectorAll(cssSelector: string)
```

Example usage:

```js
// <div id="page-body">...</div>
let pageBody = document.querySelector('div#page-body')

// [ <div class="highlight">...</div>, <div class="highlight">...</div>, ... ]
let allDivs = document.querySelectorAll('div.highlight')
```



