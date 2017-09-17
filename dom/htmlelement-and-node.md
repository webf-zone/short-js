# HTMLElement and Node

![](/assets/htmlelement-and-node.png)

The diagram shows the hierarchy of interfaces in a browser implemenation of DOM.

In the above DOM structure, the two DOM properties of the `<H1>` element \(1\) `.children` and \(2\) `.childNodes` provide different results:

![](/assets/children-and-childnodes.png)

There are 12 different types of `Nodes`, out of which 5 are deprecated \(![](/assets/deprecated.png)\). `HTMLElement` is a `Node` of type `1 (ELEMENT_NODE)`**.**

![](/assets/node-types.png)

In other words, every `HTMLElement` is a `Node` but not vice versa. The most common type of `Node` which is not a `HTMLElement` is a `TEXT_NODE`.

