---
layout: post
title: "CQL – SRW and SRU"
date: 2020-05-15 22:36:57 +0200
category: tutorial
tagline: ""
tags: [CQL, SRW, SRU]
abstract : "An overview of CQL and the SRW/SRU search protocols."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [References](#references)


# Introduction

## CQL

CQL (the **Common Query Language**,  
<http://www.loc.gov/cql/>) is an abstract and extensible query language designed to provide maximum interoperability between systems, with minimal difficulty to learn and use, while still supporting complex search requirements.

## SRW

SRW (<http://www.loc.gov/z3950/agency/>) stands for **Search/Retrieve Web Service**. It is a protocol intended to integrate access to various networked resources and promote interoperability between distributed databases by providing a common usage framework. SRW is a web-service-based protocol that combines more than 20 years of experience from the Z39.50 Information Retrieval protocol with modern web technologies.

SRW is **SOAP-based**.

## SRU

SRU (**Search/Retrieve via URL**) is a standard search protocol for Internet search queries. It also utilizes CQL as its standard query syntax for representing queries.

SRU uses **HTTP** as its transport mechanism.


# References

1. [https://www.openoffice.org/bibliographic/srw.html](https://www.openoffice.org/bibliographic/srw.html){:target="_blank"}
