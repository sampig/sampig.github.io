---
layout: post
title: "DOM Selectors Comparison - YUI vs jQuery vs JS"
date: 2020-04-14 21:55:00 +0200
category: tutorial
tagline: ""
tags: [DOM, YUI, jQuery, JavaScript]
abstract : "Compare the DOM selectors."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [DOM Selectors Comparison](#dom-selectors-comparison)
* [References](#references)


# Introduction

This article compares **DOM selector usage across three approaches**:

- **Native JavaScript**, using native DOM APIs
- **jQuery**, a widely adopted library that simplified cross-browser DOM operations
- **YUI 3**, a modular JavaScript framework that introduced a structured Node-based API

The purpose of this comparison is to highlight **syntax differences, API design choices, and conceptual similarities** when selecting and navigating DOM elements.


# DOM Selectors Comparison

| # | Description | JavaScript | jQuery 1.8 | YUI 3.0 | Notes |
|---|-------------|------------|------------|---------|-------|
| 1 | Select first element by class | `document.getElementsByClassName("eClass")[0];` | `$(".eClass:first");` | `Y.one(".eClass");` | |
| 2 | Select element by ID | `document.getElementById("elementId");` | `$("#elementId");` | `Y.one("#elementId");` | |
| 3 | Select all elements by class |  |  | `node.all(".eClass");` | |
| 4 | Get sibling elements |  | `element.siblings();` | `node.siblings();` | |
| 5 | Get next sibling |  | `element.next();` | `node.next();` | |
| 6 | Get previous sibling |  | `element.prev();` | `node.previous();` | |
| 7 | Get ancestor element |  |  | `node.ancestor();` | |



# References

1. [https://yuilibrary.com/yui/docs/node/](https://yuilibrary.com/yui/docs/node/){:target="_blank"}
2. [https://www.w3schools.com/js/js_jquery_selectors.asp](https://www.w3schools.com/js/js_jquery_selectors.asp){:target="_blank"}
3. [https://alloyui.com/rosetta-stone/](https://alloyui.com/rosetta-stone/){:target="_blank"}
