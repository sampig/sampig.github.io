---
layout: post
title: "Shell: bash vs zsh"
date: 2023-06-13 22:18:55 +0200
category: tutorial
tagline: ""
tags: [Shell, bash, zsh]
abstract: "Comparison of built-in commands between bash and zsh, focusing on history behavior."
---
{% include JB/setup %}

* [Built-in Commands](#built-in-commands)
  * [history](#history)
* [References](#references)


# Built-in Commands

## history

By default:

- **zsh**:
  - `history` lists only the **15 most recent** history entries
  - `history 1` lists **all** entries (see below)
- **bash**:
  - `history` lists **all** history entries

With numbers:

- **zsh**:
  - `history <n>` shows all entries **starting with `<n>`**, therefore  
    `history 1` shows *all* entries
  - `history -<n>` (note the `-`) shows the **`<n>` most recent** entries  
    (default behavior is effectively `history -15`)
- **bash**:
  - `history <n>` shows the **`<n>` most recent** entries
  - Bash does **not** support listing history *from* an entry number directly  
    (`fc -l <n>` requires the entry `<n>` to exist)

Optional background info:

- In **zsh**, `history` is effectively (not literally) an alias for `fc -l`
  - See: `man zshbuiltins`
  - For advanced features: `man zshall`
- In **bash**, `history` is its own command with syntax different from `fc -l`
  - See: `man bash`
- Both shells support: `fc -l <fromNum> [<toNum>]` to list a given range of history entries:
  - bash: <fromNum> must exist
  - zsh: works as long as at least one entry is in range
  - Result: fc -l 1 works in zsh (lists all), but usually not in bash


# References

1. [StackOverflow – bash vs zsh history](https://stackoverflow.com/a/26848769){:target=”_blank”}
