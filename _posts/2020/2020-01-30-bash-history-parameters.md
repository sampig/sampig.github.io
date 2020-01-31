---
layout: post
title: "Bash History Parameters"
date: 2020-01-30 22:15:00 +0200
category: tutorial
tagline: ""
tags: [Linux, Bash]
abstract : "Learning Bash: history parameters."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [History Parameters](#history-parameters)
* [Some Examples](#some-examples)
* [References](#references)


# Introduction

Bash is a powerful command language. There are so many books and many  Here I just introduced some useful history parameters.


# History Parameters

1. The last parameter: `!$`.
It will be replaced by the last parameter in the last command.
2. The n-th parameter: `!:n`.
`n` starts from 0. Then `!:0` is the command itself in the last command and `!:1` is the first parameter in the last command.
3. All parameters: `!:1-$`.
It will be replaced by all the parameters in the last command.
Subset parameters: `!:n-m`.
It will be replaced by n-th to m-th parameters.
4. The last parameter in the last n-th line: `!-n:$`.
Sometimes, we need to run other commands before re-run a history command. In this case, `!-n:$` will be helpful. `!-2:$` means the last parameter in the command before the last one.
5. The directory of the parameter: `!$:h`.
If the last parameter in the last command is a file in a full path, `!$:h` will help us get the directory of that parameter.
6. The n-th parameter in current line: `!#:n`.
It will be replaced by the n-th parameter in the current command. It helps a lot when we want to create a backup file.
7. Find and replace: `!!:gs`.
The full usage is `!!:gs/search_string/replace_string`. It will search a string in all the parameters in the last command and replace them with another string.


# Some Examples

```bash
cp /from/path/file_wrong_name /to/path/filename
# cp: cannot stat '/from/path/file_wrong_name': No such file or directory
cp /from/path/file_right_name !$

tar -cvf folder_name tar_name.tar
# tar: failed to open
!:0 !:1 !:3 !:2

pong -c 4 www.google.com
# No command 'pong' found
ping !:1-$

cp /from/path/file_wrong_name /to/path/filename
# cp: cannot stat '/from/path/file_wrong_name': No such file or directory
ls /from/path
# file_right_name
cp /from/path/file_right_name !-2:$

cat /from/path/file_wrong_name
# cat: /from/path/file_wrong_name: No such file or directory
ll !$:h
ll !-2:h

cp /path/file_original !#:1.bak
# cp /path/file_original /path/file_original.bak

echo this is tsutsu.
!!:gs/ts/zh/
# echo this is zhuzhu.
```


# References

1. [Bash Reference Manual - 9.3 History Expansion](https://www.gnu.org/software/bash/manual/bash.html#History-Interaction){:target="_blank"}
