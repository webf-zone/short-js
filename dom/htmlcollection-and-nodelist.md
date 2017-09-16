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

Although the contents of both lists are same, HTMLCollection is a live list - if the DOM gets updated, so will the HTMLCollection.

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

## Consequences

When there are chances of the DOM getting updated during the execution of a program, one should be cautious about using HTMLCollections.



