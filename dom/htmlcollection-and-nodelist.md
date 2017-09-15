# HTMLCollection and NodeList

_&lt;WIP&gt;: Work in progress_

HTMLCollection is a list of elements of type HTMLElement and while NodeList is a list of elements of type Node. HTMLCollection is a live list which gets updated upon DOM changes while NodeList is a snapshot list created and returned at the time of invocation.

```
<p id="my_paragraph">
  Some text goes here and <img src="path-of-an-image.png" />
</p>
```

In the above DOM structure

```js
var myParagraph = document.querySelector("#my_paragraph");    
var myHTMLCollection = myParagraph.children;                // [<img>]
var myNodes = myParagraph.childNodes;                       // [text, <img>]
```

`myHTMLCollection`will hold elements only of type HTMLElement. And `myNodes`will hold elements of type Node.

The native HTMLElement class is extended from the native class Node. In an HTML DOM, there are around 11 types of Nodes \(Ref: MDN web docs [Node.nodeType](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType)\).

## Usage

## Consequences



