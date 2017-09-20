# HTMLElement and Node

The word **Node** can be referred back to Telecommunications Networks - _a device such as a computer or switch attached to a computer or telecommunications network, or a point in a network topology where lines intersect or terminate_. From there, it probably arrived in XML to represent any type of entity in a document e.g. a Comment node, a Text node, an Element node etc. Similarly, the representation of HTML DOM has various entities like tags, text content, comments, attributes etc. - all these are called **Nodes**.

With respect to HTML DOM, there are 12 different types of `Nodes`, out of which 5 are deprecated \(![](/assets/deprecated.png)\). `HTMLElement` is a `Node` of type `1 (ELEMENT_NODE)`**.**

![](/assets/node-types.png)

To construct these Nodes and build the DOM Tree, the browser implementations have Interfaces. The chain of these interfaces start at `Object` as the root.

![](/assets/htmlelement-and-node.png)

Let's take an example to illustrate this.

```
<html>
    <head>
        <title>Document Title</title>
    </head>
    <body>
        <h1>Some heading</h1>
        <hr />
        <p>Paragraph text goes here.</p>
    </body>
</html>
```

In the above DOM structure, `<H1>`is an instance of `HTMLHeadingElement`. The properties available on `<H1>` instance would be inherited in a fashion - `HTMLHeadingElement` &lt;&lt; `HTMLElement` &lt;&lt; `Element` &lt;&lt; `Node` &lt;&lt; `EventTarget` &lt;&lt; `Object`. For example, the two DOM properties of the `<H1>` element \(1\) `.childNodes` and \(2\) `.children` are inherited from `Node`. Another interesting thing about these two similar sounding properties is the difference between their results. The former will list _any_ type of `Node` \(one text node, in this case\) and the later will list `Node`only of type `1 (ELEMENT_NODE)` \(none, in this case\).

![](/assets/children-and-childnodes.png)

To summarize, every `HTMLElement` is a `Node` but not vice versa. The most common type of `Node` which is not an `HTMLElement` is `TEXT_NODE`.

