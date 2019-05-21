---
layout: post
title: "Learning Latex: List of Mathematical Symbols"
date: 2019-04-28 22:15:00 +0200
category: tutorial
tagline: ""
tags: [Latex]
abstract : "Learning Note: list of mathematical symbols in Latex."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Binary Operations](#binary-operations)
* [Delimiters](#delimiters)
* [Geometry Notation](#geometry-notation)
* [Greek Letters](#greek-letters)
* [Relation Operators](#relation-operators)
* [Set or Logic Notation](#set-or-logic-notation)
* [Trigonometric Functions](#trigonometric-functions)
* [References](#references)


## Introduction

In LaTeX, there are several ways to create equations:
1.  start with `\(` and end with `\)`.
2.  inside dollar symbols: `$ eq $`.
3.  use equation block:
```latex
\begin{equation}
...
\end{equation}
```

In an equation, you might need many mathematical symbols.
Some symbols are quired packages: `amsmath`, `amssymb` or `mathtools`.


## Binary Operations

| Symbol | Script | Comment |
|--------|--------|---------|
| &#177;  | \pm | plus or minus |
| &#8723; | \mp | minus or plus |
| &#215;  | \times   | multiply |
| &#247;  | \div     | divided |
| &#8727; | \ast     | asterisk |
| &#8902; | \star    |  |
| &#8224; | \dagger  |  |
| &#8225; | \ddagger | double dagger |
| &#8745; | \cap     | set intersection |
| &#8746; | \cup     | set union |
| &#8846; | \uplus   | multiset union |
| &#8851; | \sqcap   |  |
| &#8852; | \sqcup   |  |
| &#8897; | \vee     | N-ary logical or |
| &#8896; | \wedge   | N-ary logical and |
| &#8901; | \cdot    |  |
| &#8900; | \diamond |  |
| &#9651; | \bigtriangleup   |  |
| &#9661; | \bigtriangledown |  |
| &#9667; | \triangleleft    |  |
| &#9657; | \triangleright   |  |
| &#9711; | \bigcirc  |  |
| &#8226; | \bullet   |  |
| &#8768; | \wr       | Wreath product |
| &#8853; | \oplus    |  |
| &#8854; | \ominus   |  |
| &#8855; | \otimes   |  |
| &#8856; | \oslash   |  |
| &#8857; | \odot     |  |
| &#9675; | \circ     |  |
| &#8726; | \setminus |  |
| &#10815; | \amalg    | amalgamation |


## Delimiters

| Symbol | Script | | Symbol | Script |
|--------|--------|-|--------|--------|
| &#8739;  | \mid    |  | &#8741;  | `\|` or \parallel |
| /        | /       |  | &#8726;  | \backslash |
| {        | `\{`    |  | }        | `\}` |
| [        | `\[`    |  | ]        | `\]` |
| &#10216; | \langle |  | &#10217; | \rangle |
| &#8593; | \uparrow |  | &#8595; | \downarrow |
| &#8657; | \Uparrow |  | &#8659; | \Downarrow |
| &#8968; | \lceil   |  | &#8969; | \rceil |
| &#8970; | \lfloor  |  | &#8971; | \rfloor |
| &#8988; | \ulcorner |  | &#8989; | \urcorner |
| &#8990; | \llcorner |  | &#8991; | \lrcorner |


## Geometry Notation

| Symbol | Script | Comment |
|--------|--------|---------|
| ![seg_ab]({{ site.url }}/assets/images/latex_math_symbols/seg_ab.png) | \overline{\rm AB} | segment |
| ![vec_ab]({{ site.url }}/assets/images/latex_math_symbols/vec_ab.png) | \overrightarrow{\rm AB} | ray (half-line) |
| &#8736; | \angle | angle |
| &#8737; | \measuredangle | measured angle |
| &#9653; | \triangle | triangle |
| &#9633; | \square | square |


## Greek Letters

| Symbol | Script | | Symbol | Script |
|--------|--------|-|--------|--------|
|  &Alpha;&alpha; | A \alpha | | &Nu; &nu; | N \nu |
| &Beta; &beta; | B \beta |  | &Xi; &xi; | \Xi \xi |
| &Gamma; &gamma; | \Gamma \gamma |  | &Omicron; &omicron; | O o |
| &Delta; &delta; | \Delta \delta |  | &Pi; &pi; &#982; | \Pi \pi \varpi |
| &Epsilon; &epsilon; &#1013; | E \epsilon \varepsilon |  | &Rho; &rho; &#1009; | P \rho \varrho |
| &Zeta; &zeta; | Z \zeta |  | &Sigma; &sigma; &#962; | \Sigma \sigma \varsigma |
| &Eta; &eta; | H \eta |  | &Tau; &tau; | T \tau |
| &Theta; &theta; &#977; | \Theta \theta \vartheta |  | &Upsilon; &upsilon; | \Upsilon \upsilon |
| &Iota; &iota; | I \iota |  | &Phi; &#981; &phi; | \Phi \phi \varphi |
| &Kappa; &kappa; &#1008; | K \kappa \varkappa |  | &Chi; &chi; | X \chi |
| &Lambda; &lambda; | \Lambda \lambda |  | &Psi; &psi; | \Psi \psi |
| &Mu; &mu; | M \mu |  | &Omega; &omega; | \Omega \omega |


## Relation Operators

| Symbol | Script | Comment |
|--------|--------|---------|
| < | `<` | less than |
| > | `>` | greater than |
| = | = | equal to |
| &#8814; | \nless | not less than |
| &#8815; | \ngtr | not greater than |
| &#8800; | \neq \ne | not equal to |
| &#8804; | \leq \leqslant | less than or equal to |
| &#8805; | \geq \geqslant | greater than or equal to |
| &#8816; | \nleq \nleqslant | neither less than nor equal to |
| &#8817; | \ngeq \ngeqslant | neither greater than nor equal to |
| &#8810; | \ll | much less than |
| &#8811; | \gg | much greater than |
| &#8920; | \lll | very much less than |
| &#8921; | \ggg | very much greater than |
| &#8741; | \parallel | parallel to |
| &#8742; | \nparallel | not parallel to |
| &#8784; | \doteq | approaches the limit |
| &#8801; | \equiv | equivalent to |
| &#8776; | \approx | approximately equal to |
| &#8773; | \cong | congruent to or approximately equal to |
| &#8771; | \simeq | asymptotically equal to |
| &#8764; | \sim | similar to |
| &#8834; | \subset | subset of |
| &#8835; | \supset | superset of |
| &#8836; | \not\subset | not a subset of |
| &#8837; | \not\supset | not a superset of |
| &#8838; | \subseteq | subset of or equal to |
| &#8839; | \supseteq | superset of or equal to |
| &#8840; | \nsubseteq | neither a subset of nor equal to |
| &#8841; | \nsupseteq | neither a superset of nor equal to |
| &#8847; | \sqsubset | square image of |
| &#8848; | \sqsupset | square original of |
| &#8849; | \sqsubseteq | square image of or equal to |
| &#8850; | \sqsupseteq | square original of or equal to |
| &#8826; | \prec | precedes |
| &#8827; | \succ | succeeds |
| &#8832; | \nprec | not precede |
| &#8833; | \nsucc | not succeed |
| &#8828; | \preceq | precedes or equal to |
| &#8829; | \succeq | succeeds or equal to |
| &#8928; | \npreceq | not precede or equal |
| &#8929; | \nsucceq | not succeed or equal |
| &#8733; | \propto | proportional to |
| &#8781; | \asymp | equivalent to |
| &#8904; | \bowtie | bowtie |
| &#8866; | \vdash |  |
| &#8867; | \dashv |  |
| &#8712; | \in | element of |
| &#8715; | \ni | contains as member |
| &#8713; | \notin | not an element of |
| &#8995; | \smile |  |
| &#8994; | \frown |  |
| &#8871; | \models |  |
| &#8869; | \perp |  |
| &#8739; | \mid |  |
| &#8757; | \because |  |
| &#8756; | \therefore |  |


## Set or Logic Notation

| Symbol | Script | Comment |
|--------|--------|---------|
| &#8709; | \emptyset \varnothing | empty set |
| &#8469; | \mathbb{N} | set of natural numbers |
| &#8484; | \mathbb{Z} | set of integers |
| &#8474; | \mathbb{Q} | set of rational numbers |
| &#8477; | \mathbb{R} | set of real numbers |
| &#8450; | \mathbb{C} | set of complex numbers |
| &#120120; | \mathbb{A} | set of algebraic numbers |
| &#8461; | \mathbb{H} | set of quaternions |
| &#120134; | \mathbb{O} | set of octonions |
| &#120138; | \mathbb{S} | set of sedenions |
| &#8712; | \in | element of |
| &#8715; | \ni | contains as member |
| &#8713; | \notin | not an element of |
| &#8834; | \subset | subset of |
| &#8835; | \supset | superset of |
| &#8836; | \not\subset | not a subset of |
| &#8837; | \not\supset | not a superset of |
| &#8838; | \subseteq | subset of or equal to |
| &#8839; | \supseteq | superset of or equal to |
| &#8840; | \nsubseteq | neither a subset of nor equal to |
| &#8841; | \nsupseteq | neither a superset of nor equal to |
| &#8745; | \cap     | set intersection |
| &#8746; | \cup     | set union |
| &#8726; | \setminus | set difference |
| &#8707; | \exists | there exists |
| &#8708; | \nexists | there does not exist |
| &#8704; | \forall | for all |
| &#172; | \neg | logical not |
| &#8743; | \land | logical and |
| &#8744; | \lor | logical or |
| &#8592; | \leftarrow |  |
| &#8594; | \rightarrow |  |
| &#8596; | \leftrightarrow |  |
| &#8614; | \mapsto |  |
| &#10236; | \longmapsto |  |
| &#10232; | \Longleftarrow |  |
| &#8656; | \Leftarrow |  |
| &#10233; | \Longrightarrow |  |
| &#8658; | \Rightarrow |  |
| &#10234; | \iff |  |
| &#8660; | \Leftrightarrow |  |
| &#8868; | \top |  |
| &#8869; | \bot |  |
| &#8636; | \leftharpoonup |  |
| &#8640; | \rightharpoonup |  |
| &#8637; | \leftharpoondown |  |
| &#8641; | \rightharpoondown |  |
| &#8651; | \leftrightharpoons |  |
| &#8652; | \rightleftharpoons |  |


## Trigonometric Functions

| Symbol | Script | | Symbol | Script |
|--------|--------|-|--------|--------|
| sin | \sin |  | cos | \cos |
| tan | \tan |  | cot | \cot |
| arcsin | \arcsin |  | arccos | \arccos |
| arctan | \arctan |  | arccot | \arccot |
| sinh | \sinh |  | cosh | \cosh |
| tanh | \tanh |  | coth | \coth |
| sec | \sec |  | csc | \csc |


## References

1. [LaTeX](https://www.latex-project.org/){:target="_blank"}
2. [User's Guide for the amsmath Package](https://www.latex-project.org/help/documentation/amsldoc.pdf){:target="_blank"}
3. [HTML Character Sets](https://www.w3schools.com/charsets/default.asp){:target="_blank"}
4. [detexify](http://detexify.kirelabs.org/){:target="_blank"}: applet for looking up LaTeX symbols by drawing them.
5. [Online LaTeX Equation Editor](https://www.codecogs.com/latex/eqneditor.php){:target="_blank"}
6. [Math symbols defined by LaTeX package «amssymb»](http://milde.users.sourceforge.net/LUCR/Math/mathpackages/amssymb-symbols.pdf){:target="_blank"}
