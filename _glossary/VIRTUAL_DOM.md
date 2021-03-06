---
title: Virtual DOM
excerpt: a pattern in which a JavaScript representation of the desired DOM is created and the framework sorts out the details of how to make it happen
---

# Virtual DOM

The Virtual DOM is a concept pioneered by [React](/_glossary/REACT.md) but since duplicated in other places including in [its own library](https://github.com/Matt-Esch/virtual-dom). With Virtual DOM, rather than modifying the [DOM](/_glossary/DOM.md) directly (or through some library), you create a set of JavaScript objects that represent the DOM that you would like. A simplistic example might be something like this

```js
{
   nodeType: "DIV",
   className: "container hero",
   children: [
     {
      nodeType: "H1",
      chidren: [
        {
          nodeType: "TEXT",
          textContents: "Welcome!!!",
      ],
   ],
}
```

When rendering, this model gets modified (and is often regenerated fully) by application code and passed to a diffing algorithm to identify what needs to change. These changes are then passed to the library which applies them to the DOM.

The Virtual DOM is therefore:

* Method(s) for creating this JavaScript representation of the visual tree
* A diffing algorithm
* A set of handlers which can apply patches generated by the diffing algorithm

This approach can have significant peformance benefits as the library can optimize rendering in ways that browsers would have difficulty with; for example by batching changes together or chosing to not apply a change if it is undone by one further along in the batch.

Virtual DOM is also known for granting code-maintainability benefits. Typically the Virtual DOM is immutable and regenerated fully every time any change is made. Therefore, at its heart, all of rendering is a single function that transforms an input of application state to a Virtual DOM tree. This statelessness can make debugging and testing of rendering code very straightforward as you only need to consider the input and output, not any previously rendered states.

A final benefit, is that since the Virtual DOM representation is just JavaScript, it can be output in formats other than a sequence of DOM manipulations. For example isomorphic JavaScript will render it as an HTML string which can be returned from a web request with the client-side app effectively "running" on the server (useful for loading the first page as rapidly as possible or for clients with JavaScript disabled).
