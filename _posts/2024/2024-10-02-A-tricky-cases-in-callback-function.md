---
layout: post
title: "A Tricky Cases in Callback Function"
date: 2024-10-02 19:50:32 +0200
category: tutorial
tagline: ""
tags: [JavaScript]
abstract : "Common pitfalls when using callback functions in JavaScript."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Callback Function in Array.map](#callback-function-in-arraymap)
  * [Why This Happens Internally](#why-this-happens-internally)
* [References](#references)


# Introduction

A **callback** function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

This article highlights one common and subtle pitfall involving callback functions when using `Array.prototype.map`.


# Callback Function in Array.map

A common mistake occurs when using `parseInt` directly as the callback function for `Array.map`.

**Wrong:**

```js
['1', '5', '11'].map(parseInt); // ❌
```

Output:

```
[1, NaN, 3]
```

Right:

```js
['1', '5', '11'].map(n => parseInt(n)); // ✅
```

## Why This Happens Internally

The map method invokes its callback with three arguments on each iteration:

```js
callback(element, index, array)
```

When parseInt is passed directly, it receives these arguments unintentionally:

```js
parseInt('1', 0);  // radix 0 → inferred as base 10
parseInt('5', 1);  // radix 1 → invalid → NaN
parseInt('11', 2); // radix 2 → binary → 3
```

Because parseInt treats its second argument as the radix, the index value causes incorrect parsing. Wrapping parseInt inside another function ensures that only the intended argument is passed.


# Callback Function in Promise

I also found this, but I cannot tell the difference.

```js
async function setTimeout() {
  await new Promise((resolve) => setTimeout(resolve, 1000));
  console.log('Coding Beauty');
}

async function setTimeout() {
  await new Promise((resolve) => setTimeout(() => resolve(), 1000));
  console.log('Coding Beauty');
}
```


# References

1. [MDN - Array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map){:target=”_blank”}
2. [MDN - parseInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt){:target=”_blank”}
3. [MDN - Callback function](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function){:target=”_blank”}
