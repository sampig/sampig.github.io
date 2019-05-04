---
layout: post
title: "Web Scraping - Beautiful Soup"
date: 2019-04-12 19:00:00 +0200
category: tutorial
tagline: ""
tags: [Python]
abstract : "Learning Note: using Beautiful Soup to scrap."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Objects in Beautiful Soup](#objects-in-beautiful-soup)
* [Navigating the Tree](#navigating-the-tree)
* [Searching the Tree](#searching-the-tree)
    - [Method: find_all()](#method-find_all)
    - [Method: find()](#method-find)
    - [Other Methods](#other-methods)
* [Example](#example)
* [References](#references)


## Introduction

Before reading it, please read the warnings in my blog [_Learning Python: Web Scraping_]({{ site.url }}/tutorial/2019/04/11/learning-python-web-scraping#introduction){:target="_blank"}.

A brief introduction of [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/){:target="_blank"} can be found in my blog [_Learning Python: Web and Databases_]({{ site.url }}/tutorial/2019/02/09/learning-python-web-db#beautifulsoup){:target="_blank"}.
It creates a parse tree for parsed pages that can be used to extract data from HTML, which is useful for web scraping.

Create a BeautifulSoup object that represents the document as a nested data structure.
```python
#!/usr/bin/env python3

from bs4 import BeautifulSoup
import urllib.request

url = "https://kassiesa.home.xs4all.nl/bert/uefa/data/method5/match2018.html"
request = urllib.request.Request(url)
response = urllib.request.urlopen(request, timeout=20)
content = response.read()

soup = BeautifulSoup(content, "html.parser")
with open(filename, "wb") as f:
    f.write(soup)
```

Beautiful Soup supports the HTML parser included in Python's standard library, but it also supports a number of third-party Python parsers. One is the [lxml parser](https://lxml.de/){:target="_blank"}. For instance, `BeautifulSoup(markup, "lxml")`.
It is very fast and lenient.

## Objects in Beautiful Soup

Beautiful Soup transforms a complex HTML document into a complex tree of Python objects.
The objects are mainly four kinds: `Tag`, `NavigableString`, `BeautifulSoup`, and `Comment`.
1. `BeautifulSoup`: the BeautifulSoup object itself represents the document as a whole.
2. `Tag`: a Tag object corresponds to an XML or HTML tag in the original document. Every tag has a name (accessible as `.name`) and any number of attributes (accessible by treating like a dictionary).
3. `NavigableString`: a string corresponds to a bit of text within a tag. You can't edit a string in place, but you can replace one string with another, using `replace_with()`.
4. `Comment`: the Comment object is just a special type of NavigableString.

```python
title = soup.title

print(type(title))
print(title.name)

print(title)
print(title.string)
```

Beautiful Soup defines classes for anything else that might show up in an XML document: `CData`, `ProcessingInstruction`, `Declaration`, and `Doctype`.

## Navigating the Tree

In a HTML/XML document, tag may contain texts and other tags.
Beautiful Soup provides many attributes for navigating and iterating over tree.
1. Directly use the name of the tag. Using a tag name as an attribute will give you only the first tag by that name.
2. `.contents` give a list of a tag's direct children.
3. `.children` generator can be used to iterate over a tag's direct children.
4. `.descendants` allows to iterate over all of a tag's children recursively including its direct children, the children of its direct children and so on.
5. `.string` gives the text in this tag if it has only one NavigableString child. It gives the text in a tag's child if this tag has only one tag child and this tag child has a string. If a tag contains more than one thing, it is no clear and is defined to be `None`.
6. `.parent` can access an element's parent.
7. `.parents` can iterate over all of an element's parents.
8. `.next_sibling` and `.previous_sibling` can navigate between elements that are on the same level.
9. `.next_siblings` and `.previous_siblings` can iterate over a tag's siblings.
10. `.next_element` and `.previous_element` can navigate to the next or previous element of a tag. It is different from `.next_sibling` and `.previous_sibling`.

```python
print(soup.head)
print(soup.head.title)
```

```python
body = soup.body
print(type(body.contents))
print(len(body.contents))
print(type(body.children))
print(len(list(body.children)))
print(type(body.descendants))
print(len(list(body.descendants)))
```

```python
print(soup.title.parent)
print(type(soup.html.parent))

for parent in soup.title.parents:
    if parent is None:
        print(parent)
    else:
        print(parent.name)
```

```python
body = soup.body
print(body.table)

print(body.table.next_sibling.next_sibling)
print(body.table.next_sibling.previous_sibling)

print(body.table.next_element)
print(body.table.tr.previous_element)
```

## Searching the Tree

Beautiful Soup also provides many methods for searching the tree.
Two main methods are `find()` and `find_all()`.

Some basic usage of the methods:
1. use a string;
```python
print(soup.find_all("style"))
print(len(soup.find_all("table")))
```
2. use regular expression;
```python
import re
print(len(soup.find_all(re.compile("^b"))))
```
3. use a list;
```python
print(len(soup.find_all(["tr", "td"])))
```
4. use `True`;
```python
print(len(soup.find_all(True)))
```
5. use a self defined function.
```python
def has_class_but_no_id(tag):
       return tag.has_attr("class") and not tag.has_attr("id")
print(len(soup.find_all(has_class_but_no_id)))
```

There are some arguments for these two methods to use.

### Method: find_all()

`find_all(name, attrs, recursive, string, limit, **kwargs)`:
1. `name`: it can be a string, a regular expression, a list a function or `True`.
2. `attrs`: Any argument that's not recognized will be turned into a filter on one of a tag's attributes. Sometimes, the attributes cannot be used as a keyword argument. Then use `attrs` to pass attribute name and its value. It would be a little different if you want to search by CSS class. It uses the keyword argument `class_`.
```python
# attributes
print(len(soup.find_all(align="center")))
print(len(soup.find_all(attrs={"attr-name": "attr-value"})))
# class attributes
print(len(soup.find_all(class_="lgray")))
print(len(soup.find_all(attrs={"class": "lgray"})))
```
3. `recursive`: if you set this value to False like `recursive=False`, it will only search through the direct children instead of all the descendants.
4. `string`: with it you can search for strings instead of tags. It also accepts a string, a regular expression, a list, a function or `True`.
```python
soup.find_all(string="Juventus")
```
5. `limit`: it limits the number of results.
```python
soup.find_all(string="Juventus", limit=3)
```

### Method: find()

`find(name, attrs, recursive, string, **kwargs)`: it only returns the first result.
If `find()` can't find anything, it returns `None` instead of an empty list.

### Other Methods

There are some other methods: `find_parents()`, `find_parent()`, `find_next_siblings()`, `find_next_sibling()`, `find_previous_siblings()`, `find_previous_sibling()`, `find_all_next()`, `find_next()`, `find_all_previous()` and `find_previous()`. They are all similar. So I will not describe them in detail here.

As of version 4.7.0, Beautiful Soup supports most CSS4 selectors via the [SoupSieve](https://facelessuser.github.io/soupsieve/){:target="_blank"} project.


## Example

[KassiesA: UEFA European Cup Football](https://kassiesa.home.xs4all.nl/bert/uefa/index.html){:target="_blank"} contains a lot of soccer data for the matches of UEFA Champions League and Europa League.

I will give an example using Beautiful Soup to extract the results of all the matches in [UEFA European Cup Matches 2017/2018](https://kassiesa.home.xs4all.nl/bert/uefa/data/method5/match2018.html){:target="_blank"}.

The HTML content in the page looks like:
```html
<tr class="blue">
<th colspan="6" style="padding: 0;">
<div style="line-height: 56px; border: 2px solid #999999;">
CHAMPIONS LEAGUE
</div>
</th></tr>
...
<tr class="yellow">
<th colspan="6" style="padding: 0;">
<div style="line-height: 36px; border: 2px solid #999999;">
Final
</div>
</th></tr>
...
<tr class="lgray">
<td><b>Real Madrid</b></td>
<td>Esp</td>
<td>Liverpool</td>
<td>Eng</td>
<td align="center">3-1</td>
<td align="center"> </td>
</tr>
```

Based on the structure of the page, I develop a simple program to save all the match results in file with CSV format.

```python
#!/usr/bin/env python3

from bs4 import BeautifulSoup
import urllib.request

url = "https://kassiesa.home.xs4all.nl/bert/uefa/data/method5/match2018.html"
request = urllib.request.Request(url)
response = urllib.request.urlopen(request, timeout=20)
content = response.read()

soup = BeautifulSoup(content, "html.parser")

for table in soup.find_all("table", class_="t1"):
    game_type = table.find("tr", class_="blue").div.string.strip()
    if game_type == "CHAMPIONS LEAGUE":
        filename = "cl.txt"
    elif game_type == "EUROPA LEAGUE":
        filename = "el.txt"
    for row in table.find_all("tr"):
        if row["class"][0] == "yellow":
            round_type = row.div.string.strip()
            with open(filename, "a") as f:
                f.write(round_type + "\n")
        elif row["class"][0] == "lgray":
            result = ""
            for td in row.find_all("td"):
                if td.string.strip() != "":
                    result += td.string.strip() + ","
            with open(filename, "a") as f:
                f.write(result[:-1] + "\n")
```

Some parts of the file:
```
Semi Finals
Bayern München,Ger,Real Madrid,Esp,1-2,2-2
Liverpool,Eng,AS Roma,Ita,5-2,2-4

Final
Real Madrid,Esp,Liverpool,Eng,3-1
```

Then we can use them for our own analysis.


## Further

Besides parsing tree, Beautiful Soup also allows to modify the tree and write the changes as a new HTML or XML document.

More information in detail can be found in [Beautiful Soup Official Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/){:target="_blank"}.


## References

1. [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/){:target="_blank"}
2. [KassiesA: UEFA European Cup Football](https://kassiesa.home.xs4all.nl/bert/uefa/index.html){:target="_blank"}
