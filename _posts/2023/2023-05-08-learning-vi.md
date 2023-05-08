---
layout: post
title: "Learning vi"
date: 2023-05-08 20:16:35 +0200
category: tutorial
tagline: ""
tags: [Linux, vi]
abstract : "Notes and basic commands for learning the vi editor."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Basic](#basic)
* [Move Cursor](#move-cursor)
* [Basic Text Editing](#basic-text-editing)
* [Undo, Delete, Yank, and Put](#undo-delete-yank-and-put)
* [Search and Replace](#search-and-replace)
* [Advanced Editing Features](#advanced-editing-features)
* [References](#references)

# Introduction

This document contains learning notes for **vi**, based on practical usage and a LinkedIn online course <https://www.linkedin.com/learning/learning-vi?u=2209602>. It summarizes essential commands, modes, cursor movement, and editing techniques that are useful for beginners getting started with vi.

# Basic

Save and quit:

```text
[Shift] + zz
:wq
:q!
```

Modes:

```text
Command mode
i I a A o O c

Insert mode
[Esc]

Prompt mode
: / ! ?
[Return]
```

Other basics:

```text
Double [Esc]      Cancel command input
[Ctrl] + l        Redraw screen
:N                Go to previous file
:rew              Rewind to first file
:r                Read file into current file
[Ctrl] + g        Display line number and file status
```


# Move Cursor

Basic movement:

```text
H J K L
Arrow keys
[Space]           Forward
[Backspace]       Backward
[Return]          Beginning of next line
-                 Beginning of previous line
```

Word and sentence movement:

```text
w     Forward a word
b     Backward a word
e     Forward to end of word

)     Forward a sentence
(     Backward a sentence
}     Forward a paragraph
{     Backward a paragraph
```

Line and file navigation:

```text
^     Beginning of line
$     End of line
1G    First line of file
G     Last line of file
nG    Go to line n
%     Move to matching bracket
```

Scrolling:

```text
[Ctrl] + e        Scroll down one line
[Ctrl] + y        Scroll up one line
[Ctrl] + d / u    Down / up half screen
[Ctrl] + f / b    Down / up full screen
```


# Basic Text Editing

Insert text:

```text
i     Insert before cursor
I     Insert at beginning of line
a     Append after cursor
A     Append at end of line
o     Open new line below
O     Open new line above
```

Delete text:

```text
x     Delete current character
dd    Delete current line
dw    Delete current word
de    Delete to end of word
d^    Delete to beginning of line
d$    Delete to end of line
D     Delete to end of line
```

(d can be combined with any movement command and a number.)

Change text:

```text
r     Replace character (command mode)
s     Replace character (insert mode)
cc    Change current line
cw    Change word
ce    Change to end of word
c^    Change to beginning of line
c$    Change to end of line
C     Change to end of line
```

Other editing commands:

```text
R     Overwrite mode
~     Toggle character case
J     Join next line to current line
```


# Undo, Delete, Yank, and Put

Undo and repeat:

```text
u         Undo last change
[Ctrl] + r  Redo last change
U         Undo all changes on current line
.         Repeat last change
```

Delete, yank, and put:

```text
dd    Delete (cut) line
yy    Yank (copy) line
dx    Delete amount
yx    Yank amount
p     Put after cursor
P     Put before cursor
```

Notes:

- Deletes and yanks use vi’s internal buffer, not the OS clipboard
- `y` can use number or any movement command


# Search and Replace

Will be finished in the future.


# Advanced Editing Features

Will be finished in the future.


# References

1. [LinkedIn - Learning vi](https://www.linkedin.com/learning/learning-vi?u=2209602){:target="_blank"}
