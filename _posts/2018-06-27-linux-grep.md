---
layout: post
title: "Linux Command: grep"
date: 2018-06-27 23:00:00 +0100
category: tutorial
tagline: ""
tags: [Linux]
---
{% include JB/setup %}

> Type: Linux **search** command.

* [Introduction](#introduction)
* [Basic Usage](#basic-usage)
  * [Options](#options)
  * [_grep_ Programs](#grep-programs)
* [Regular Expressions](#regular-expressions)
  * [Fundamental Structure](#fundamental-structure)
  * [Character Classes and Bracket Expressions](#character-classes-and-bracket-expressions)
  * [Backslash Character and Special Expressions](#backslash-character-and-special-expressions)
  * [Anchoring](#anchoring)
  * [Extended Regular Expressions](#extended-regular-expressions)
* [Examples](#examples)
  * [Basic Examples](#basic-examples)
  * [Regular Expressions Examples](#regular-expressions-examples)
  * [Extended Regular Expressions Examples](#extended-regular-expressions-examples)
  * [Other Examples](#other-examples)
* [References](#references)

## Introduction

"_grep_" stands for "_global/regular expression/print_".

_grep_ is a command used to search text for lines that match the given pattern in input files and print out the matching lines.

There are no limits on input lines but available memory.

## Basic Usage

A general usage:

```
grep [OPTIONS]... PATTERN [FILES]...
```

### Options

There are several types of options.

#### Generic Program Information

__--help__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print the help text.

__-V__, __--version__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print version information.

#### Matching control.

__-e PATTERN__, __--regexp=PATTERN__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;use PATTERN for matching.

__-f FILE__, __--file=FILE__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;obtain patterns from FILE, one per line.

__-i__, __-y__, __--ignore-case__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;ignore case distinctions.

__-v__, __--invert-match__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;select non-matching lines.

__-w__, __--word-regexp__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;force PATTERN to match only whole words.

__-x__, __--line-regexp__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;force PATTERN to match only whole lines.

#### General Output Control

__-c__, __--count__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print only a count of matching lines per FILE.

__--color[=WHEN]__, __--colour[=WHEN]__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;use markers to highlight the matching strings; WHEN is '_always_', '_never_' or '_auto_'.

__-L__, __--files-without-match__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp; print only names of FILEs containing no match.

__-l__, __--files-with-match__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print only names of FILEs containing matches.

__-m NUM__, __--max-count=NUM__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;stop after NUM matches.

__-o__, __--only-matching__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;show only the part of a line matching PATTERN.

__-q__, __--quiet__, __--silent__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;suppress all normal output.

__-s__, __--no-messages__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;suppress error messages.

#### Output Line Prefix Control

__-b__, __--byte-offset__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print the byte offset with output lines.

__-H__, __--with-filename__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print the file name for each match.

__-h__, __--no-filename__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;suppress the file name prefix on output.

__--label=LABEL__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;use LABEL as the standard input file name prefix.

__-n__, __--line-number__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print line number with output lines.

__-T__, __--initial-tab__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;make tabs line up (if needed).

__-u__, __--unix-byte-offsets__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;report offsets as if CRs were not there (MSDOS/Windows).

__-Z__, __--null__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print 0 byte after FILE name.

#### Context Line Control

__-A NUM__, __--after-context=NUM__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print NUM lines of training context.

__-B NUM__, __--before-context=NUM__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print NUM lines of leading context.

__-C NUM__, __-NUM__, __--context=NUM__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;print NUM lines of output context.

#### File and Directory Selection

__--binary-file=TYPE__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;assume that binary files are TYPE; TYPE is 'binary', 'text' or 'without-match'.

__-a__, __--text__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;equivalent to _--binary-files=text_.

__-I__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;equivalent to _--binary-files=without-match_.

__-D ACTION__, __--devices-ACTION__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;how to handle devices, FIFOs and sockets; ACTION is 'read' or 'skip'.

__-d ACTION__, __--directories=ACTION__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;how to handle directories; ACTION is 'read', 'recurse' or 'skip'.

__--exclude=FILE\_PATTERN__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;skip files and directories matching FILE\_PATTERN.

__--include=FILE\_PATTERN__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;search only files that match FILE\_PATTERN.

__--exclude-from=FILE__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;skip files matching any file pattern from FILE.

__--exclude-dir=PATTERN__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;directories that match PATTERN will be skipped.

__-r__, __--recursive__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;operand, read and process all files in that directory recursively for each directory. Like '_--directories=recurse_'.

__-R__, __--dereference-recursive__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;operand, read and process all files in that directory recursively, following all symbolic links for each directory.

#### Other Options

__--line-buffered__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;flush output on every line.

__-U__, __--binary__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;do not strip CR characters at EOL (MSDOS/Windows).

__-z__, __--null-data__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;a data line ends in 0 byte, not newline.

### _grep_ Programs

There are 4 major variants of _grep_:

__-G__, __--basic-regexp__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;PATTERN is a basic regular expression (BRE)

__-E__, __--extended-regexp__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;PATTERN is an extended regular expression (ERE)

__-F__, __--fixed-strings__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;PATTERN is a set of newline-separated strings

__-P__, __--perl-regexp__:<br/>
&nbsp; &nbsp; &nbsp; &nbsp;PATTERN is a Perl regular expression

In addition, two variant programs _egrep_ and _fgrep_ are available. _egrep_ is the same as '_grep -E_'. _fgrep_ is the same as '_grep -F_'.

## Regular Expressions

A _regular expression_ is a pattern that describes a set of strings.

### Fundamental Structure

'.'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;matches any single character.

'?'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;the preceding item is optional and will be matched at most once.

'*'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;the preceding item will be matched zero or more times.

'+'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;the preceding item will be matched one or more times.

'{n}'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;the preceding item is matched exactly _n_ times.

'{n,}'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;the preceding item is matched _n_ or more times.

'{,m}'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;the preceding item is matched at most _m_ times.

'{n,m}'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;the preceding item is matched at least _n_ times, but not more than _m_ times.

The empty regular expression matches the empty string.<br/>
Two regular expressions may be concatenated.<br/>
Two regular expressions may be joined by the infix operator '|'.

### Character Classes and Bracket Expressions

A _bracket expression_ is a list of character enclosed by '[' and ']'.<br/>
It matches any single character in that list; if the first character of the list is the caret '^', then it matches any character not in the list.

'[:alnum:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;alphanumeric characters: '[:alpha:]' and '[:digit:]'; in the 'c' locale and ASCII character encoding, this is the same as '[0-9A-Za-z]'.

'[:alpha:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;alphabetic characters: '[:lower:]' and '[:upper:]'; in the 'c' locale and ASCII character encoding, this is the same as '[A-Za-z]'.

'[:blank:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;blank characters: space and tab.

'[:cntrl:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;control character. In ASCII, these characters have octal codes 000 through 037, and 177 (DEL).

'[:digit:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;digits: 0-9

'[:graph:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;graphical characters: '[:alnum:]' and '[:punct:]'.

'[:lower:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;lower-case letters.

'[:print:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;printable characters: '[:alnum:]', '[:punct:]' and space.

'[:punct:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;punctuation characters. In the 'c' locale and ASCII character encoding, this includes _! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~_.

'[:space:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;space characters: in the 'c' locale, this includes tab, newline, vertical tab, form feed, carriage return and space.

'[:upper:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;upper-case letters.

'[:xdigit:]'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;hexadecimal digits: 0-9 A-F a-f.

### Backslash Character and Special Expressions

'\b'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;match the empty string at the edge of a word.

'\B'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;match the empty string provided it is not at the edge of a word.

'\\<'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;match the empty string at the beginning of word.

'\\>'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;match the empty string at the end of word.

'\w'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;match word constituent, it is a synonym for '[_[:alnum:]]'.

'\W'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;match non-word constituent, it is a synonym for '[^_[:alnum:]]'.

'\s'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;match whitespace, it is a synonym for '[[:space:]]'.

'\S'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;match non-whitespace, it is a synonym for '[^[:space:]]'.

### Anchoring

The caret '^' matches the beginning of a line.<br/>
The dollar sign '$' matches the end of a line.

### Extended Regular Expressions

'|'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;alternation. Expression can be chosen between more than 2 choices by additional pip characters.

'()'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;grouping.

'{}'<br/>
&nbsp; &nbsp; &nbsp; &nbsp;specifies match repetition. The brace characters can specify the number of times that a match is repeated.

## Examples

Use the GPL file in the common licenses directory as an example.
```
cd /usr/share/common-licenses
```

### Basic Examples

The output of the result will be every line containing the pattern text:
```
grep "GNU" GPL-3
```

The output of this result will be every line containing the word "license" (with any mixed cases):
```
grep -i "license" GPL-3
```

The output of the result will be the lines that do NOT contain the word "the":
```
grep -v "the" GPL-3
```

The output of the result will be the matching lines including the line numbers:
```
grep -n "the" GPL-3
```

### Regular Expressions Examples

Only match "GNU" if it occurs at the beginning of a line:
```
grep "^GNU" GPL-3
```

Only match "and" if it occurs at the end of a line:
```
grep "and$" GPL-3
```

Match anything that has 2 characters and then the string "cept":
```
grep "..cept" GPL-3
```

Find the lines that contain "too" or "two":
```
grep "t[wo]o" GPL-3
```

Find the pattern ".ode" but not match "code":
```
grep "[^c]ode" GPL-3
```

Find lines that begin with a capital letter:
```
grep "^[A-Z]" GPL-3
grep "^[[:upper:]]" GPL-3
```

Find lines that contain an opening and closing parenthesis, with only letters and single spaces in between:
```
grep "([A-Za-z ]*)" GPL-3
```

Find lines that begin with a capital letter and end with a period:
```
grep "^[A-Z].*\.$" GPL-3
```

### Extended Regular Expressions Examples

Find either "GPL" or "General Public License" in the text:
```
grep -E "(GPL|General Public License)" GPL-3
```

Find lines that match "copyright" and "right":
```
grep -E "(copy)?right" GPL-3
```

Find lines that contain the string "free" plus one or more characters that are not whitespace (such as "freedom" and "free."):
```
grep -E "free[^[:space:]]+" GPL-3
```

Find lines that contain any words that have between 16 and 20 characters:
```
grep -E "[[:alpha:]]{16,20}" GPL-3
```

### Other Examples

List just the names of matching files:
```
grep -l "GPL" *
```

Search directories recursively:
```
grep -r "GPL" .
```

Search for a whole word instead of a part of a word:
```
grep -w "GPL" *
```

Output context around the matching lines:
```
grep -C 2 "GPL" *
```

Force to print the name of the file:
```
grep "GPL" GPL-3 /dev/null
grep -H "GPL" GPL-3
```

## References

1. [GNU grep home page](https://www.gnu.org/software/grep/)
2. [GNU Grep 3.0](https://www.gnu.org/software/grep/manual/grep.html)
