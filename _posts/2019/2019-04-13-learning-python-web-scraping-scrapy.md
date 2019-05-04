---
layout: post
title: "Web Scraping - Scrapy"
date: 2019-04-13 19:00:00 +0200
category: tutorial
tagline: ""
tags: [Python]
abstract : "Learning Note: using Scrapy to scrap."
---
{% include JB/setup %}

* [Introduction](#introduction)
    - [Basic Usage](#basic-usage)
    - [Create a Project](#create-a-project)
    - [Running Spider](#running-spider)
    - [Extracting Data](#extracting-data)
* [Example](#example)
* [Further](#further)
* [References](#references)


## Introduction

Before reading it, please read the warnings in my blog [_Learning Python: Web Scraping_]({{ site.url }}/tutorial/2019/04/11/learning-python-web-scraping#introduction){:target="_blank"}.

Scrapy is an application framework for crawling web sites and extracting structured data which can be used for a wide range of useful applications, like data mining, information processing or historical archival.
You can install Scrapy via `pip`.

> Don't use the python-scrapy package provided by Ubuntu, they are typically too old and slow to catch up with latest Scrapy.
> Instead, use `pip install scrapy` to install.

### Basic Usage

After installation, try `python3 -m scrapy --help` and get help information:
```
Scrapy 1.6.0 - no active project

Usage:
  scrapy <command> [options] [args]

Available commands:
  bench         Run quick benchmark test
  fetch         Fetch a URL using the Scrapy downloader
  genspider     Generate new spider using pre-defined templates
  runspider     Run a self-contained spider (without creating a project)
  settings      Get settings values
  shell         Interactive scraping console
  startproject  Create new project
  version       Print Scrapy version
  view          Open URL in browser, as seen by Scrapy

  [ more ]      More commands available when run from project directory

Use "scrapy <command> -h" to see more info about a command
```

A basic flow of Scrapy usage:
1. Create a new Scrapy project.
2. Write a spider to crawl a site and extract data.
3. Export the scraped data using the command line.
4. Change spider to recursively follow links.
5. Try to use other spider arguments.

### Create a Project

Create a new Scrapy project:
```
python3 -m scrapy startproject soccer
```

Then it will create a directory like:
```
soccer/
  ├─scrapy.cfg          # deploy configuration file
  └─soccer/             # project's Python module, you'll import your code from here
      ├─__init__.py
      ├─items.py        # project items definition file
      ├─middlewares.py  # project middlewares file
      ├─pipelines.py    # project pipelines file
      ├─settings.py     # project settings file
      └─spiders/        # a directory where you'll later put your spiders
          └─__init__.py
```

Create a class of our own spider which is the subclass of `scrapy.Spider` in the file `soccer_spider.py` under the `soccer/spiders` directory.

```python
#!/usr/bin/env python3

import scrapy


class SoccerSpider(scrapy.Spider):
    name = "soccer"

    def start_requests(self):
        urls = [
            "https://kassiesa.home.xs4all.nl/bert/uefa/data/method5/match2018.html",
            "https://kassiesa.home.xs4all.nl/bert/uefa/data/method4/match2017.html"
        ]
        for url in urls:
            yield scrapy.Request(url=url, callback=self.parse)

    def parse(self, response):
        page = response.url.split("/")[-2]
        filename = "soccer-ucl-%s.html" % page
        with open(filename, "wb") as f:
            f.write(response.body)
        self.log("Saved file %s" % filename)

```

- `name`: identifies the Spider. It must be unique within a project.
- `start_requests()`: must return an iterable of Requests which the Spider will begin to crawl from.
- `parse()`: a method that will be called to handle the response downloaded for each of the requests made.
- Scrapy schedules the `scrapy.Request` objects returned by the `start_requests` method of the Spider.

### Running Spider

Go to the `soccer` root directory and run the spider using `runspider` or `crawl` commands:
```
python3 -m scrapy runspider soccer/spiders/soccer_spider.py
```
```
python3 -m scrapy crawl soccer
```

When getting the page content in `response.body` or in a local saved file, you could use other libraries such as Beautiful Soup to parse it.
Here, I will continue use the methods provided by Scrapy to parse the content.

### Extracting Data

Scrapy provides CSS selectors `.css()` and XPath `.xpath()` for the `response` object. Some examples:
```python
response.css("title")
response.css("title").getall()
response.css("title").get()
response.css("::text").re(r"Juventus")

response.xpath("//title")
```

With that, you can extract the data according to the elements, CSS styles or XPath. Add the codes in the `parse()` method.

Sometimes, you may want to extract the data from another link in the page.
Then you can find the link and get the response by sending another request like:
```python
next_page = response.css("li.next a::attr('href')").get()
if next_page is not None:
    next_page = response.urljoin(next_page)
    yield scrapy.Request(next_page, callback=self.parse)
```

Use the `.urljoin()` method to build a full absolute URL (since sometimes the links can be relative).

Scrapy also provides another method `.follow()` that supports relative URLs directly.
```python
for href in response.css('li.next a::attr(href)'):
    yield response.follow(href, callback=self.parse)
```


## Example

I will still use the data in [UEFA European Cup Matches 2017/2018](https://kassiesa.home.xs4all.nl/bert/uefa/data/method5/match2018.html){:target="_blank"} as an example.

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

I developed a new class extends the `scrapy.Spider` class and then run it via Scrapy to extract the data.

```python
#!/usr/bin/env python3

import scrapy


class SoccerSpider(scrapy.Spider):
    name = "soccer"

    def start_requests(self):
        urls = [
            "https://kassiesa.home.xs4all.nl/bert/uefa/data/method5/match2018.html",
            "https://kassiesa.home.xs4all.nl/bert/uefa/data/method4/match2017.html"
        ]
        for url in urls:
            yield scrapy.Request(url=url, callback=self.parse)

    def parse(self, response):
        page = response.url.split("/")[-1]

        # save the page
        filename = "soccer-uefa-%s" % page
        with open(filename, "wb") as f:
            f.write(response.body)
        self.log("Saved file %s" % filename)

        # extract data
        prefix = page.split(".")[0]
        for table in response.xpath("//table[@class='t1']"):
            game_type = table.xpath("./tr[@class='blue']//div/text()").get().strip()
            if game_type == "CHAMPIONS LEAGUE":
                filename = prefix + "_" + "cl.txt"
            elif game_type == "EUROPA LEAGUE":
                filename = prefix + "_" + "el.txt"
            for row in table.xpath("./tr"):
                if row.xpath("./@class").get().strip() == "yellow":
                    round_type = row.xpath(".//div/text()").get().strip()
                    with open(filename, "a") as f:
                        f.write(round_type + "\n")
                elif row.xpath("./@class").get().strip() == "lgray":
                    result = ""
                    for td in row.xpath("./td"):
                        if td.xpath(".//text()").get().strip() != "":
                            result += td.xpath(".//text()").get().strip() + ","
                    with open(filename, "a") as f:
                        f.write(result[:-1] + "\n")
```

I prefer using XPath because it is more flexible.
Learn more about XPath in [XML and XPath in W3Schools](https://www.w3schools.com/xml/xml_xpath.asp){:target="_blank"} or other tutorials.


## Further

You can use other shell commands such as `python3 -m scrapy shell 'URL'` to do some testing job before writing your own spider.

More information about Scrapy in detail can be found in [Scrapy Official Documentation](https://docs.scrapy.org/){:target="_blank"} or its [GitHub](https://github.com/scrapy/scrapy){:target="_blank"}.


## References

1. [Scrapy](https://scrapy.org/){:target="_blank"}
2. [KassiesA: UEFA European Cup Football](https://kassiesa.home.xs4all.nl/bert/uefa/index.html){:target="_blank"}
