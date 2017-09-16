# Finding DOM Elements

Front-end world before jQuery was completely different ballgame. Finding any DOM element within HTML page was cumbersome. You had only three options:

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

Doing this with CSS is simple one liner:

```css
div.highlight p { color: yellow; }
```

Back then, people wished if there could be a way as simple as using CSS selector. Enter jQuery and world changed for better. This  cumbersome four step process reduced to single line:

```js
jQuery('div.highlight p').css('color', 'yellow');
```

At that time, jQuery became de facto; it was used by more than 50% websites around the world. And as such, it is one of the classic question discussed in interview: **Change colors of all paragraphs who are children of div element having class highlight "using plain JavaScript"**. And I am still waiting for a person to come up with an answer.

## Selector API

jQuery left a big legacy behind and as such jQuery inspired **Selector API** is proof of that legacy. You can use **selector API** to do what jQuery is doing:

```js
// Returns first matching element that matches the specified selector
// Returns null if no matching element found
document.querySelector(cssSelector: string)

// Returns list of DOM nodes containing all elements that matches the selector
// Returns empty list if no elements are found
document.querySelectorAll(cssSelector: string)
```

Example usage:

```js
// <div id="page-body">...</div>
let pageBody = document.querySelector('div#page-body')

// [ <div class="highlight">...</div>, <div class="highlight">...</div>, ... ]
let allDivs = document.querySelectorAll('div.highlight')
```

Additionally `querySelector`and `querySelectorAll`is available not just on document object but also on every html element. In that case it will search for element within subtree of that element:

```js
/* HTML structure
<div id="sample">
    <p>Hello</p>
    <div><p></p></div>
</div>
<div><p></p></div>
*/

// Select <div id="sample">
let divElement = document.querySelector('#sample');

// Select all `p` that are descendent
let para = divElement.querySelectorAll('p');

console.log(para.length);    // 2
```

## Uses

In 2017, it should be remembered that **web is not SPA and SPA is not web**. Not everything is a web application. We have enormous number of websites that needs a bit of JavaScript for interaction. At such places, you may use jQuery or plain JavaScript. That is where you can use **selector API**.

Front-end ecosystem has grown exponentially. Many beginners are picking up so called buzz words - Angular, React, Vue - instead of learning core concepts of web \(HTML + CSS + JS\). These buzz words are just one of the many amazing things you can do with JavaScript. But you will not get anywhere beyond a framework if you do not understand fundamental concepts of web.

### Further reading

Web applications vs Websites

DOM, Nodes, etc.

