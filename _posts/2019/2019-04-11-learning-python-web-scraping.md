---
layout: post
title: "Learning Python: Web Scraping"
date: 2019-04-11 18:15:00 +0200
category: tutorial
tagline: ""
tags: [Python]
abstract : "Learning Note: list some modules such as Beautiful Soup or Scrapy for web scraping."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Scraping Tools](#scraping-tools)
* [Scraping Flow](#scraping-flow)
* [Summary](#summary)
* [References](#references)


## Introduction

In my previous blog [_Datasets for Machine Learning_]({{ site.url }}/tutorial/2019/03/13/datasets-for-machine-learning){:target="_blank"}, I introduced many datasets for machine learning.
However, you might not be able to find a dataset that is suitable for your own research or project.
The data that you need are published online but not archived.
In this case, you need to scrap those data by your own.
Of course, if you want to use these scraping data for a commercial purpose, you should take action carefully and seriously in a legal way.

__Warning!!!__

Please pay attention to the below:
1. Read the terns and conditions about the data usage in the website you want to scrap.
2. Once getting the permission, be polite and friendly when scraping data. DO NOT send too frequently requests to the website in order to avoid increasing too much unnecessary pressure to the server.
3. After scraping the data, use them legally.


## Scraping Tools

Here are some tools or libraries in Python or Python-supported for web scraping:
1. [__BeautifulSoup__](https://www.crummy.com/software/BeautifulSoup/){:target="_blank"}: a Python package for parsing HTML and XML documents.
2. [__Scrapy__](https://scrapy.org/){:target="_blank"}: an open source, collaborative, fast and high-level web crawling & scraping framework for extracting the data from websites in a fast, simple, yet extensible way.
3. [__pyspider__](http://docs.pyspider.org/){:target="_blank"}: a powerful spider(web crawler) system in Python.
4. [pyquery](https://pypi.org/project/pyquery/){:target="_blank"}: a jquery-like library that allows to make jquery queries on xml documents.
5. [webscraping](https://pypi.org/project/webscraping/){:target="_blank"}: a library for web scraping or website navigation.
6. [Selenium](https://www.seleniumhq.org/){:target="_blank"}: a suite of tools to automate web browsers across many platforms.


## Scraping Flow

1. Before scraping, be sure and clear that the data are useful for your analysis. Otherwise, you will just get some useless data and waste your time.
2. Explore the structure of the website or page. Here are two websites that provide data about soccer: [KassiesA: UEFA European Cup Football](https://kassiesa.home.xs4all.nl/bert/uefa/index.html){:target="_blank"} and [Football-Data.co.uk](http://www.football-data.co.uk/){:target="_blank"}.
3. Based on the structure, write your own spider with the libraries to extract the data that you want.
4. Save the data locally well for analysis.


## Summary

Those libraries and tools are powerful and easy to use.
I will describe how to use some of those libraries or tools in detail in the future.


## References

1. [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/){:target="_blank"}
2. [Scrapy](https://scrapy.org/){:target="_blank"}
3. [pyspider](http://docs.pyspider.org/){:target="_blank"}
4. [pyquery](https://pypi.org/project/pyquery/){:target="_blank"}
5. [webscraping](https://pypi.org/project/webscraping/){:target="_blank"}
6. [Selenium](https://www.seleniumhq.org/){:target="_blank"}

[](){:target="_blank"}
[](){:target="_blank"}
