---
layout: post
title: "Font Resources"
date: 2023-07-30 02:16:10 +0200
category: tutorial
tagline: ""
tags: [Font]
abstract : "A collection of useful resources for working with fonts, PDF generation, Unicode text processing, and web typography."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [PDFBox & Fonts](#pdfbox--fonts)
* [Font Repositories](#font-repositories)
* [Unicode & Text Processing](#unicode--text-processing)
* [CSS & Web Fonts](#css--web-fonts)
* [Font Embedding](#font-embedding)
* [Bidirectional Text (Bidi) & RTL](#bidirectional-text-bidi--rtl)
* [References](#references)

# Introduction

This post compiles useful resources for working with fonts, PDF generation, Unicode text processing, and web typography. Whether you're dealing with Arabic text in PDFs, implementing web fonts, or working with Unicode normalization, these resources provide essential information and tools.

# PDFBox & Fonts

## Arabic Text in PDFBox
- [Writing Arabic with PDFBOX with correct characters presentation form without being separated](https://stackoverflow.com/questions/48284888/writing-arabic-with-pdfbox-with-correct-characters-presentation-form-without-bei){:target="_blank"}
- [How To Display Arabic Text in PDFBox](https://stackoverflow.com/questions/38047110/how-to-display-arabic-text-in-pdfbox){:target="_blank"}
- [Hebrew, Arabic, Yiddish text is written in reverse order in PDFBox 2.0.5](https://stackoverflow.com/questions/44136960/hebrew-arabic-yiddish-text-is-written-in-reverse-order-in-pdfbox-2-0-5){:target="_blank"}

## PDFBox Documentation & Examples
- [PDFBox Document Creation](https://pdfbox.apache.org/1.8/cookbook/documentcreation.html){:target="_blank"}
- [PDFBox Working with Fonts](https://pdfbox.apache.org/1.8/cookbook/workingwithfonts.html){:target="_blank"}
- [PDFBox 2.0 Font Encoding FAQ](https://pdfbox.apache.org/2.0/faq.html#fontencoding){:target="_blank"}
- [PDFBox Source Code](https://github.com/apache/pdfbox){:target="_blank"}
- [PDFBox Examples - EmbeddedFonts.java](https://github.com/apache/pdfbox/blob/trunk/examples/src/main/java/org/apache/pdfbox/examples/pdmodel/EmbeddedFonts.java){:target="_blank"}
- [PDFBox Examples - CreateSimpleFormWithEmbeddedFont.java](https://svn.apache.org/viewvc/pdfbox/trunk/examples/src/main/java/org/apache/pdfbox/examples/interactive/form/CreateSimpleFormWithEmbeddedFont.java?view=markup){:target="_blank"}

## Unicode Text in PDFBox
- [Generation of PDF from HTML with non-Latin characters using ITextRenderer does not work](https://stackoverflow.com/questions/10250606/generation-of-pdf-from-html-with-non-latin-characters-using-itextrenderer-does-n){:target="_blank"}
- [How to write unicode text to pdf with pdfbox?](https://stackoverflow.com/questions/25525213/how-to-write-unicode-text-to-pdf-with-pdfbox){:target="_blank"}
- [Using Java PDFBox library to write Russian PDF](https://stackoverflow.com/questions/1713751/using-java-pdfbox-library-to-write-russian-pdf){:target="_blank"}
- [PDFBox "special" characters in Helvetica](https://stackoverflow.com/questions/33637295/pdfbox-special-characters-in-helvetica){:target="_blank"}

# Font Repositories

## Google Fonts
- [Google Fonts](https://fonts.google.com/){:target="_blank"}
- [Noto Fonts](https://fonts.google.com/noto){:target="_blank"}
- [Noto Fonts Source](https://github.com/notofonts/noto-source){:target="_blank"}

## Liberation Fonts
- [Liberation Fonts](https://github.com/liberationfonts/liberation-fonts){:target="_blank"}

## Adobe Fonts
- [Adobe Fonts GitHub](https://github.com/adobe-fonts?page=2){:target="_blank"}
- [Adobe Blank](https://github.com/adobe-fonts/adobe-blank){:target="_blank"}
- [Adobe notdef](https://github.com/adobe-fonts/adobe-notdef){:target="_blank"}

## Adobe Type Tools
- [Adobe Font Development Kit for OpenType (AFDKO)](https://github.com/adobe-type-tools/afdko/){:target="_blank"}

# Unicode & Text Processing

## Unicode Standards
- [Unicode Home](https://home.unicode.org/){:target="_blank"}
- [Unicode Normalization (TR15)](https://www.unicode.org/reports/tr15/){:target="_blank"}
- [Unicode Charts](http://unicode.org/charts/){:target="_blank"}
- [Unicode Character Lookup](https://unicode.scarfboy.com/?s=U%2B1E25){:target="_blank"}
- [Unicode Character Info](https://www.fileformat.info/info/unicode/char/1e25/index.htm){:target="_blank"}

## Combining Diacritical Marks 组合附加符号
- [Combining Diacritical Marks (English)](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks){:target="_blank"}
- [Combining Diacritical Marks (中文)](https://zh.wikipedia.org/wiki/%E7%B5%84%E5%90%88%E9%99%84%E5%8A%A0%E7%AC%A6%E8%99%9F){:target="_blank"}
- [Unicode FAQ: Characters and Combining Marks](http://unicode.org/faq/char_combmark.html){:target="_blank"}

## Unicode Processing
- [Remove accents/diacritics in a string in JavaScript](https://stackoverflow.com/questions/990904/remove-accents-diacritics-in-a-string-in-javascript){:target="_blank"}
- [How to combine unicode characters?](https://stackoverflow.com/questions/9707656/how-to-combine-unicode-characters){:target="_blank"}
- [How to convert Combining Diacritical Marks to single grapheme](https://stackoverflow.com/questions/48523029/how-to-convert-combining-diacritical-marks-to-single-grapheme){:target="_blank"}
- [Composing unicode characters in Java?](https://stackoverflow.com/questions/11058470/composing-unicode-characters-in-java){:target="_blank"}
- [Algorithm to check for combining characters in Unicode](https://stackoverflow.com/questions/17051732/algorithm-to-check-for-combining-characters-in-unicode){:target="_blank"}
- [Normalizing Text (Java Tutorial)](https://docs.oracle.com/javase/tutorial/i18n/text/normalizerapi.html){:target="_blank"}
- [Unicode equivalence](https://en.wikipedia.org/wiki/Unicode_equivalence){:target="_blank"}

## Text Processing
- [Split on non arabic characters](https://stackoverflow.com/questions/20856213/split-on-non-arabic-characters){:target="_blank"}

# CSS & Web Fonts

## Font Stacks & Fallbacks
- [CSS Basics: Fallback Font Stacks for More Robust Web Typography](https://css-tricks.com/css-basics-fallback-font-stacks-robust-web-typography/){:target="_blank"}
- [System Font Stack](https://css-tricks.com/snippets/css/system-font-stack/){:target="_blank"}
- [CSS Font Stack](https://www.cssfontstack.com/){:target="_blank"}
- [CSS Font Stack - Century Gothic](https://www.cssfontstack.com/Century-Gothic){:target="_blank"}
- [CSS Font Stack - Calibri](https://www.cssfontstack.com/Calibri){:target="_blank"}
- [CSS Font Stack - Trebuchet MS](https://www.cssfontstack.com/Trebuchet-MS){:target="_blank"}

## @font-face
- [How to use @font-face in CSS](https://css-tricks.com/snippets/css/using-font-face-in-css/){:target="_blank"}
- [Unicode range in @font-face](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/unicode-range){:target="_blank"}
- [The importance of `@font-face` source order when used with preload](https://nooshu.com/blog/2021/01/23/the-importance-of-font-face-source-order-when-used-with-preload/){:target="_blank"}
- [When using CSS @font-face, in what order do browsers use the different types?](https://stackoverflow.com/questions/21154219/when-using-css-font-face-in-what-order-do-browsers-use-the-different-types){:target="_blank"}

## Web Font Optimization
- [Optimize WebFont loading and rendering](https://web.dev/articles/optimize-webfont-loading){:target="_blank"}

## Google Fonts CSS
- [Noto Sans SC CSS](https://fonts.googleapis.com/css2?family=Noto+Sans+SC&display=swap){:target="_blank"}

# Font Embedding

- [Difference between full embedded fonts and embedded subset](https://publicatorcommunity.getfastr.com/hc/en-us/articles/115002482043-Difference-between-full-embedded-fonts-and-embedded-subset){:target="_blank"}

## iText
- [iText eBooks](https://kb.itextpdf.com/itext/ebooks){:target="_blank"}

# Bidirectional Text (Bidi) & RTL

- [ICU Bidi API Documentation](https://unicode-org.github.io/icu-docs/apidoc/dev/icu4j/com/ibm/icu/text/Bidi.html){:target="_blank"}
- [Improving Arabic and Hebrew text in map labels](https://blog.mapbox.com/improving-arabic-and-hebrew-text-in-map-labels-fd184cf5ebd1){:target="_blank"}

# References

1. [PDFBox](https://github.com/apache/pdfbox){:target="_blank"}
2. [Google Fonts](https://fonts.google.com/){:target="_blank"}
3. [Unicode Consortium](https://home.unicode.org/){:target="_blank"}
4. [CSS-Tricks](https://css-tricks.com/){:target="_blank"}
5. [Adobe Type Tools](https://github.com/adobe-type-tools/afdko/){:target="_blank"}
