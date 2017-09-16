# HTMLCollection and NodeList

```
<div id="myContent">
    <p>First paragraph</p>
    <p>Second paragraph</p>
    <p>Third paragraph</p>
    <p>Fourth paragraph</p>
</div>
```

With the above HTML structure, the DOM API document.getElementsByTagName\("p"\) will return an array-like list called HTMLCollection while document.querySelectorAll\("p"\) will also return an array-like list called NodeList.

| DOM API | Result |
| :--- | :--- |
| document.getElementsByTagName\("p"\) | ![](/assets/HTMLCollection.png) |
|  |  |
| document.querySelectorAll\("p"\) | ![](/assets/NodeList.png) |

Although the contents of both lists are same, HTMLCollection is always a live list - if the corresponding DOM gets updated, so will the HTMLCollection.

```js
var myContent = document.querySelector("#myContent");
var myHTMLCollection = myContent.getElementsByTagName("p");
var myNodeList = myContent.querySelectorAll("p");
var newParagraph = document.createElement("p");

console.log(myHTMLCollection.length);    // 4
console.log(myNodeList.length);          // 4

myContent.appendChild(newParagraph);

console.log(myHTMLCollection.length);    // 5 - live list reflects the current state of DOM
console.log(myNodeList.length);          // 4
```

It is also possible to get hold of a live NodeList; e.g. &lt;HTMLElement&gt;.childNodes.

Today, the concept of HTMLCollection \_probably \_exists in modern browser implementations just for legacy purposes - to retain the behavior of older and now non-standard DOM APIs like document.forms, &lt;HTMLElement&gt;.children, document.getElementsByTagName\(\) etc.

## A word of caution about live collections

As an example of live collections, Node.childNodes returns a live NodeList and document.getElementsByTagName\(\) returns a live HTMLCollection. One should be extra careful while iterating on these entities, as an operation that updates the same collection from within the iteration might affect the length of the loop in an unexpected way.

