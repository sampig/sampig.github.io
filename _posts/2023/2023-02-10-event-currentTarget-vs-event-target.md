---
layout: post
title: "JavaScript: event.currentTarget vs event.target"
date: 2023-02-10 14:23:28 +0200
category: tutorial
tagline: ""
tags: [JavaScript]
abstract : "Understanding the difference between event.target and event.currentTarget in JavaScript."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Example](#example)
* [References](#references)


# Introduction

In the DOM event system, two commonly confused properties are **`event.target`** and **`event.currentTarget`**. Understanding the difference between them is essential when working with **event propagation**, especially during the **capturing** and **bubbling** phases.

> The read-only **`target`** property of the `Event` interface is a reference to the object onto which the event was originally dispatched.  
> It differs from **`Event.currentTarget`** when the event handler is invoked during the bubbling or capturing phase.
>
> The **`currentTarget`** property identifies the element whose event listener is currently being executed.  
> It always refers to the element the handler is attached to, while `target` may refer to a descendant element where the event originated.

Event propagation works in two phases:

- **Capturing phase** — event travels from ancestor → descendant  
- **Bubbling phase** — event travels from descendant → ancestor


# Example

```html
<html>
<head>
  <title>event.currentTarget vs event.target</title>
</head>
<body>

<div id="a">a
  <div id="b">b
    <div id="c">c
      <div id="d">d</div>
    </div>
  </div>
</div>

<div id="w">w
  <div id="x">x
    <div id="y">y
      <div id="z">z</div>
    </div>
  </div>
</div>

<script>
  var useCapture = true;
  document.getElementById('a').addEventListener('click', clickFunc, useCapture);
  document.getElementById('b').addEventListener('click', clickFunc, useCapture);
  document.getElementById('c').addEventListener('click', clickFunc, useCapture);
  document.getElementById('d').addEventListener('click', clickFunc, useCapture);

  useCapture = false;
  document.getElementById('w').addEventListener('click', clickFunc, useCapture);
  document.getElementById('x').addEventListener('click', clickFunc, useCapture);
  document.getElementById('y').addEventListener('click', clickFunc, useCapture);
  document.getElementById('z').addEventListener('click', clickFunc, useCapture);

  function clickFunc(e) {
    var text = 'target:' + e.target.id + ', currentTarget:' + e.currentTarget.id;
    console.log(text);
  }
</script>

</body>
</html>
```

When clicking **d** (capturing phase):

```text
target:d, currentTarget:a
target:d, currentTarget:b
target:d, currentTarget:c
target:d, currentTarget:d
```

When clicking **z** (bubbling phase):

```text
target:z, currentTarget:z
target:z, currentTarget:y
target:z, currentTarget:x
target:z, currentTarget:w
```

# References

1. [https://developer.mozilla.org/en-US/docs/Web/API/Event/currentTarget](https://developer.mozilla.org/en-US/docs/Web/API/Event/currentTarget){:target="_blank"}
2. [https://developer.mozilla.org/en-US/docs/Web/API/Event/target](https://developer.mozilla.org/en-US/docs/Web/API/Event/target){:target="_blank"}
3. [https://developer.mozilla.org/en-US/docs/Web/API/Event/Comparison_of_Event_Targets](https://developer.mozilla.org/en-US/docs/Web/API/Event/Comparison_of_Event_Targets){:target="_blank"}
4. [https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_bubbling](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_bubbling){:target="_blank"}
5. [https://www.quirksmode.org/js/events_order.html](https://www.quirksmode.org/js/events_order.html){:target="_blank"}
