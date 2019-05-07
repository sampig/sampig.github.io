---
layout: post
title: "Learning Python: Web and Databases"
date: 2019-02-09 15:00:00 +0100
category: tutorial
tagline: ""
tags: [Python]
abstract : "Learning Note: web applications creation with web frameworks and database connections."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Web Frameworks](#web-frameworks)
    - [Django](#django)
    - [TurboGears](#turbogears)
    - [web2py](#web2py)
    - [Werkzeug](#werkzeug)
    - [Bottle](#bottle)
    - [CherryPy](#cherrypy)
    - [Flask](#flask)
    - [Web Components](#web-components)
    - [Web Applications](#web-applications)
* [Web Client Programming](#web-client-programming)
    - [httplib](#httplib)
    - [urllib](#urllib)
    - [BeautifulSoup](#beautifulsoup)
* [Databases](#databases)
    - [MySQL](#mysql)
    - [PostgreSQL](#postgresql)
    - [SQLite](#sqlite)
    - [buzhug](#buzhug)
* [References](#references)


## Introduction

Web programming contains several aspects: servers, clients and databases.

Below is only a simple introduction to basic usage of some of these modules. Because web programming covers too many topics.
I would introduce some of the modules in detail in separate blogs in the future.


## Web Frameworks

A web framework is a collection of packages or modules which allow to write web applications or services without having  to handle such low-level details as protocols, sockets or process/thread management.

Frameworks provides support for web activities such as interpreting requests, producing responses, storing data and so on. Some full-stack frameworks could provide a complete solution.

Full-stack frameworks:
1. [Django](https://www.djangoproject.com/){:target="_blank"}: it is a high-level Python Web framework that encourages rapid development and clean, pragmatic design.
2. [TurboGears](http://www.turbogears.org/){:target="_blank"}: it is a Rapid Web Application development with a slightly different focus. It combines SQLAlchemy (Model) or Ming (MongoDB Model), Genshi (view), Repoze and Tosca Widgets. TurboGears 2 is the built on top of the experience of several next generation web frameworks including TurboGears 1 (of course), Django, and Rails.
3. [web2py](http://www.web2py.com/){:target="_blank"}: it is a free open source full-stack framework for rapid development of fast, scalable, secure and portable database-driven web-based applications. Written and programmable in Python.
4. [CubicWeb](http://www.cubicweb.org/){:target="_blank"}: it is a semantic web application framework, featuring a query language named RQL, a selection+view mechanism for semi-automatic XHTML/XML/JSON/text generation, reusable components, the reliability of SQL databases, LDAP directories, Subversion and Mercurial for storage backends.
5. [wheezy.web](https://bitbucket.org/akorn/wheezy.web){:target="_blank"}: it is a lightweight, high performance, high concurrency WSGI web framework with the key features to build modern, efficient web. Its functionality includes routing, model update/validation, authentication/authorization, content caching with dependency, xsrf/resubmission protection, AJAX+JSON, i18n (gettext), middlewares, and more. Template engine agnostic (integration with jinja2, mako, tenjin and wheezy.template) plus html widgets.
6. [Zope2](http://www.zope.org/){:target="_blank"}: it is a Python-based web application server for building secure and highly scalable web applications.
7. [Werkzeug](https://palletsprojects.com/p/werkzeug/){:target="_blank"}: it is a comprehensive WSGI web application library. It is Unicode-aware, includes a powerful debugger, full featured request and response objects, HTTP utilities to handle entity tags, cache control headers, HTTP dates, cookie handling, file uploads, a powerful URL routing system and a bunch of community contributed addon modules. 

Non full-stack frameworks:
1. [Bottle](http://bottlepy.org/){:target="_blank"}: it is a fast, simple and lightweight WSGI micro web-framework for Python.
2. [CherryPy](https://cherrypy.org/){:target="_blank"}: it is a pythonic, object-oriented web development framework. 
3. [Flask](http://flask.pocoo.org/){:target="_blank"}: it is a microframework for Python based on Werkzeug and Jinja 2.
4. [Hug](https://github.com/timothycrosley/hug){:target="_blank"}: it only supports Python 3+.
5. [Pyramid](https://trypyramid.com/){:target="_blank"}: it is a small, fast, down-to-earth, open source Python web development framework.

### Django

[Django](https://www.djangoproject.com/){:target="_blank"} is a high-level Python Web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of Web development, so you can focus on writing your app without needing to reinvent the wheel. It's free and open source.

- Django provides an abstraction layer (the "models") for structuring and manipulating the data of your Web application.
- Django has the concept of "views" to encapsulate the logic responsible for processing a user's request and for returning the response.
- The template layer provides a designer-friendly syntax for rendering the information to be presented to the user.
- Django provides a rich framework to facilitate the creation of forms and the manipulation of form data.
- Django provides components and tools to help development and testing.
- Django provides an automated admin interface.
- Security is a topic of paramount importance in the development of Web applications and Django provides multiple protection tools and mechanisms.
- Django offers a robust internationalization and localization framework to assist you in the development of applications for multiple languages and world regions.
- GeoDjango intends to be a world-class geographic Web framework. Its goal is to make it as easy as possible to build GIS Web applications and harness the power of spatially enabled data.
- Django offers other tools: authentication, caching, logging, sending emails, syndication feeds, pagination, sessions, sitemaps and data validation.

### TurboGears

[TurboGears](http://www.turbogears.org/){:target="_blank"} is a Rapid Web Application development with a slightly different focus. It combines SQLAlchemy (Model) or Ming (MongoDB Model), Genshi (view), Repoze and Tosca Widgets. TurboGears 2 is the built on top of the experience of several next generation web frameworks including TurboGears 1 (of course), Django, and Rails.

- Starts as a microframework and scales up to a fullstack solution.
- Code that is as natural as writing a function.
- A powerful and flexible Object Relational Mapper (ORM) with real multi-database support.
- Support for Horizontal data partitioning (aka, sharding).
- A new widget system to make building AJAX heavy apps easier.
- Support for multiple data-exchange formats.
- Built in extensibility Pluggable Applications and standard WSGI components.
- Designer friendly template system great for programmers.

```python
#!/usr/bin/env python

from wsgiref.simple_server import make_server
from tg import MinimalApplicationConfigurator
from tg import expose, TGController

# RootController of our web app, in charge of serving content for /
class RootController(TGController):
    @expose(content_type="text/plain")
    def index(self):
        return 'Hello World'

# Configure a new minimal application with our root controller.
config = MinimalApplicationConfigurator()
config.update_blueprint({
    'root_controller': RootController()
})

# Serve the newly configured web application.
print("Serving on port 8080...")
httpd = make_server('', 8080, config.make_wsgi_app())
httpd.serve_forever()
```

### web2py

[web2py](http://www.web2py.com/){:target="_blank"} is a free open source full-stack framework for rapid development of fast, scalable, secure and portable database-driven web-based applications. Written and programmable in Python.

web2py:
1. runs with Apache, Nginx, Lighttpd, Cherokee and almost any other web server via CGI, FastCGI, WSGI, mod_proxy, and/or mod_python. It can embed third party WSGI apps and middleware.
2. talks to SQLite, PostgreSQL, MySQL, MSSQL, FireBird, Sybase, Oracle, IBM DB2, Informix, Ingres, MongoDB, and Google App Engine.
3. secure It prevents the most common types of vulnerabilities including Cross Site Scripting, Injection Flaws, and Malicious File Execution.
4. enforces good Software Engineering practices (Model-View-Controller design, Server-side form validation, postbacks) that make the code more readable, scalable, and maintainable.
5. speaks multiple protocols HTML/XML, RSS/ATOM, RTF, PDF, JSON, AJAX, XML-RPC, CSV, REST, WIKI, Flash/AMF, and Linked Data (RDF).
6. includes an SSL-enabled and streaming-capable web server, a relational database, a web-based integrated development environment and web-based management interface, a Database Abstraction Layer that writes SQL for you in real time, internationalization support, multiple authentication methods, role based access control, an error logging and ticketing system, multiple caching methods for scalability, the jQuery library for AJAX and effects, and a scaffolding application to jumpstart development.

### Werkzeug

[Werkzeug](https://palletsprojects.com/p/werkzeug/){:target="_blank"} is a comprehensive WSGI web application library. It began as a simple collection of various utilities for WSGI applications and has become one of the most advanced WSGI utility libraries.

It includes:
- An interactive debugger that allows inspecting stack traces and source code in the browser with an interactive interpreter for any frame in the stack.
- A full-featured request object with objects to interact with headers, query args, form data, files, and cookies.
- A response object that can wrap other WSGI applications and handle streaming data.
- A routing system for matching URLs to endpoints and generating URLs for endpoints, with an extensible system for capturing variables from URLs.
- HTTP utilities to handle entity tags, cache control, dates, user agents, cookies, files, and more.
- A threaded WSGI server for use while developing applications locally.
- A test client for simulating HTTP requests during testing without requiring running a server.

A simple example:
```python
#!/usr/bin/env python

from werkzeug.wrappers import Request, Response

@Request.application
def application(request):
    return Response("Hello, World!")

if __name__ == "__main__":
    from werkzeug.serving import run_simple
    run_simple("localhost", 4000, application)
```

### Bottle

[Bottle](http://bottlepy.org/){:target="_blank"} is a fast, simple and lightweight WSGI micro web-framework for Python. It is distributed as a single file module and has no dependencies other than the Python Standard Library.


- __Routing__: Requests to function-call mapping with support for clean and dynamic URLs.
- __Templates__: Fast and pythonic built-in template engine and support for mako, jinja2 and cheetah templates.
- __Utilities__: Convenient access to form data, file uploads, cookies, headers and other HTTP-related metadata.
- __Server__: Built-in HTTP development server and support for paste, fapws3, bjoern, gae, cherrypy or any other WSGI capable HTTP server.

```python
#!/usr/bin/env python

from bottle import route, run, template

@route("/hello/<name>")
def index(name):
    return template("<b>Hello {{name}}</b>!", name=name)

run(host="localhost", port=8080)
```

### CherryPy

[CherryPy](https://cherrypy.org/){:target="_blank"} is a pythonic, object-oriented web framework.

- A reliable, HTTP/1.1-compliant, WSGI thread-pooled webserver.
- Easy to run multiple HTTP servers (e.g. on multiple ports) at once.
- A powerful configuration system for developers and deployers alike.
- A flexible plugin system.
- Built-in tools for caching, encoding, sessions, authentication, static content, and many more.
- Swappable and customizable...everything.
- Built-in profiling, coverage, and testing support.
- Runs on Python 2.7+, 3.5+, PyPy, Jython and Android.

```python
#!/usr/bin/env python

import cherrypy

class HelloWorld(object):
    @cherrypy.expose
    def index(self):
        return "Hello World!"

cherrypy.quickstart(HelloWorld())
```

### Flask

[Flask](http://flask.pocoo.org/){:target="_blank"} is a micro web development framework for Python.
It depends on the [Jinja](http://jinja.pocoo.org){:target="_blank"} template engine and the [Werkzeug](http://werkzeug.palletsprojects.com/){:target="_blank"} WSGI toolkit.

```python
#!/usr/bin/env python

from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run()
```

### Web Components

Some other modules are used to solve some common problems such as authorization, form and templates.

Authorization toolkits:
1. [AuthKit](https://pypi.org/project/AuthKit/){:target="_blank"}: it is an authentication and authorization toolkit for WSGI applications and frameworks.
2. [LibAuthKit](http://isotopesoftware.ca/wiki/LibAuthKit){:target="_blank"}: it is a fork of AuthKit that provides an extensible Python framework for writing authentication and authorization backends using the WSGI specification.
3. [HTTP basic authentication example](http://code.activestate.com/recipes/305288/){:target="_blank"}: it is a CGI script demonstrating how to manually do basic authentication over http.

Form handling:
1. [FormBuild](https://pypi.org/project/FormBuild/){:target="_blank"}: it is used to generate forms quickly and easily.
2. [FormEncode](http://formencode.org/){:target="_blank"}: it is a validation and form generation package.
3. [tw.forms](http://pypi.python.org/pypi/tw.forms/){:target="_blank"}: it is a web widget for building and validating forms.

Template engines:
1. [Jinja2](http://jinja.pocoo.org/){:target="_blank"}: it is a full-featured, small, stand-alone template engine for Python.
2. [Mako](https://www.makotemplates.org/){:target="_blank"}: it is a template library that provides a familiar, non-XML syntax which compiles into Python modules for maximum performance.
3. [Clearsilver](http://www.clearsilver.net/){:target="_blank"}: it is a fast, powerful, and language-neutral HTML template system for Python/C/Perl.
4. [Ophelia](http://www.thomas-lotze.de/en/software/ophelia/){:target="_blank"}: it is a Python package that assembles XHTML pages from [TAL](https://zope.readthedocs.io/en/latest/zope2book/AppendixC.html "Template Attribute Language") templates. It is used on a web server to generate each page at the moment it is requested.
5. [Cheetah](http://cheetahtemplate.org/){:target="_blank"}: it is a Python-powered template engine and code generator.

### Web Applications

Some widely-deployed web applications written in Python:

1. Blogging
    1. [Pelican](https://blog.getpelican.com/){:target="_blank"}: it is a static site generator that generates static web pages from Markdown or reStructuredText.
    2. [PyCS - Python Community Server](https://wiki.python.org/moin/PyCS){:target="_blank"}: it is a reimplementation of the Radio Community Server in Python.
    3. [PyDS - Python Desktop Server](https://wiki.python.org/moin/PyDS){:target="_blank"}: it is a combined weblog and aggregator much in the Spirit of Radio Userland, but implemented in 100% Python. It needs a community server like PyCS or some FTP server to host its weblog.
2. Forum
    1. [Askbot](https://askbot.com/){:target="_blank"}: it is a Django/Python Q&A forum.
    2. [FlaskBB](https://www.flaskbb.org/){:target="_blank"}: it is a classic Forum Software in Python.
3. Mail Reading
    1. [PyWebMail](http://pywebmail.sourceforge.net/){:target="_blank"}: it is a POP3 interface to web mail accounts.
4. Search Engines
    1. [searx](https://asciimoo.github.io/searx/){:target="_blank"}: it is a free internet metasearch engine which aggregates results from more than 70 search services.
5. Wikis (Python-based Wiki Engines)
    1. [MoinMoin](http://moinmo.in/){:target="_blank"}: it is a wiki software implemented in Python.
    2. [Markdoc](https://github.com/zacharyvoase/markdoc){:target="_blank"}: it is a lightweight Markdown-based wiki system.
    3. [Pwyky](http://infomesh.net/pwyky/){:target="_blank"}: it is a small single file wiki in Python. The author has also written another small wiki, called [WyPy](http://infomesh.net/2003/wypy/){:target="_blank"}, that is a wiki implemented in just 11 lines of Python.
    4. [Sphene Community Tools](http://sct.sphene.net/wiki/show/Start/){:target="_blank"}: it is a Django-based forum and wiki application.
    5. [Trac](https://trac.edgewall.org/){:target="_blank"}: it is an enhanced wiki and issue tracking system for software development projects.


## Web Client Programming

There are also lots of libraries for client-side web programming:
1. [urllib](http://docs.python.org/library/urllib.html){:target="_blank"}, [urllib2](https://docs.python.org/2/library/urllib2.html){:target="_blank"} and [httplib](https://docs.python.org/2/library/httplib.html){:target="_blank"}: they are in the standard library.
2. [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/){:target="_blank"}: it is a permissive HTML parser.
3. [mxTidy](http://www.egenix.com/files/python/mxTidy.html){:target="_blank"}: it is a Python interface to [html tidy](http://tidy.sourceforge.net/){:target="_blank"} library to clean up HTML documents.
4. [html5lib](https://github.com/html5lib/html5lib-python){:target="_blank"}: it is a standards-compliant library for parsing and serializing HTML documents and fragments in Python.
5. [libxml2dom](https://pypi.org/project/libxml2dom/){:target="_blank"} can parse HTML by employing libxml2's liberal HTML parser. It provides a traditional DOM wrapper.

### httplib

The [httplib](https://docs.python.org/2/library/httplib.html){:target="_blank"} module defines classes which implement the client side of the HTTP and HTTPS protocols. It is normally not used directly - the module urllib uses it to handle URLs that use HTTP and HTTPS.

> The httplib module in Python 2 has been renamed to http.client in Python 3.

```python
#!/usr/bin/env python2

import httplib

conn = httplib.HTTPSConnection("www.python.org")
conn.request("GET", "/")
res = conn.getresponse()
print res.status, res.reason
data = res.read()
print len(data)
conn.close()
```

### urllib

The [urllib](https://docs.python.org/2/library/urllib.html){:target="_blank"} module provides a high-level interface for fetching data across the World Wide Web.

The [urllib2](https://docs.python.org/2/library/urllib2.html){:target="_blank"} module defines functions and classes which help in opening URLs (mostly HTTP) in a complex world — basic and digest authentication, redirections, cookies and more.

> The [urllib](http://docs.python.org/library/urllib.html){:target="_blank"} module in Python 2 has been split into parts and renamed in Python 3 to urllib.request, urllib.parse, and urllib.error. 

The `urllib.request` module defines functions and classes which help in opening URLs (mostly HTTP) in a complex world — basic and digest authentication, redirections, cookies and more.
The `urllib.parse` module defines functions that fall into two broad categories: URL parsing and URL quoting. 
The `urllib.error` module defines the exception classes for exceptions raised by urllib.request. The base exception class is URLError.

```python
#!/usr/bin/env python2

import urllib

opener = urllib.FancyURLopener({})
f = opener.open("http://www.python.org/")
print f.read(200)
```

```python
#!/usr/bin/env python2

import urllib2

f = urllib2.urlopen("http://www.python.org/")
print f.read(200)
```

```python
#!/usr/bin/env python3

import urllib.request

f = urllib.request.urlopen("http://www.python.org/")
print(f.read(200).decode("utf-8"))
```

### BeautifulSoup

[BeautifulSoup](www.crummy.com/software/BeautifulSoup/){:target="_blank"} is a Python library designed for quick turnaround projects like screen-scraping.

- Beautiful Soup provides a few simple methods and Pythonic idioms for navigating, searching, and modifying a parse tree: a toolkit for dissecting a document and extracting what you need. It doesn't take much code to write an application
- Beautiful Soup automatically converts incoming documents to Unicode and outgoing documents to UTF-8. You don't have to think about encodings, unless the document doesn't specify an encoding and Beautiful Soup can't detect one. Then you just have to specify the original encoding.
- Beautiful Soup sits on top of popular Python parsers like lxml and html5lib, allowing you to try out different parsing strategies or trade speed for flexibility. 

```python
#!/usr/bin/env python

from bs4 import BeautifulSoup
import urllib2

f = urllib2.urlopen("http://www.python.org/")
soup = BeautifulSoup(f.read(), "html.parser")

print soup.title
print soup.title.name
print soup.title.string

for link in soup.find_all("a"):
    print link.get("href")
```


## Databases

Some of available Python popular databases interfaces:
1. Generic DB interfaces and APIs:
    1. The Python standard for database interfaces is the [Python DB-API (PEP 249)](http://www.python.org/dev/peps/pep-0249/){:target="_blank"}. Most Python database interfaces adhere to this standard.
    2. ODBC (Open Database Connectivity) drivers: [mxODBC](https://www.egenix.com/products/python/mxODBC/){:target="_blank"}, [pyodbc](https://github.com/mkleehammer/pyodbc){:target="_blank"}, [turbodbc](https://github.com/blue-yonder/turbodbc){:target="_blank"}, [ceODBC](http://ceodbc.sourceforge.net){:target="_blank"}.
2. Drivers of Relational DBs:
    1. IBM [DB2](http://www.ibm.com/db2){:target="_blank"}: 
        [ibm_db](https://github.com/ibmdb/python-ibmdb){:target="_blank"},
        [PyDB2](https://sourceforge.net/projects/pydb2/){:target="_blank"}.
    2. [Firebird](http://firebirdsql.org/){:target="_blank"}:
        [FDB](https://fdb.readthedocs.io/en/latest/){:target="_blank"},
        [PyfirebirdSQL](https://github.com/nakagami/pyfirebirdsql){:target="_blank"}.
    3. IBM [Informix](https://www.ibm.com/analytics/informix){:target="_blank"}:
        [InformixDB](http://informixdb.sourceforge.net/){:target="_blank"},
        [ibm_db](https://github.com/ibmdb/python-ibmdb){:target="_blank"}.
    4. [MySQL](https://www.mysql.com/){:target="_blank"}: see drivers listed [below](#mysql).
    5. [Oracle](https://www.oracle.com/){:target="_blank"}: [cx_Oracle](https://oracle.github.io/python-cx_Oracle/){:target="_blank"}
    6. [PostgreSQL](https://www.postgresql.org/){:target="_blank"}: see drivers listed [below](#postgresql).
    7. [SAP DB (MaxDB)](https://www.sap.com/community/topics/maxdb.html){:target="_blank"}: [sdb.dbapi](http://maxdb.sap.com/doc/7_7/46/71b2a516ae0284e10000000a1553f6/frameset.htm){:target="_blank"}
    8. [Microsoft SQL Server](https://www.microsoft.com/en-us/sql-server){:target="_blank"}:
        [adodbapi](http://adodbapi.sourceforge.net/){:target="_blank"},
        [pymssql](http://pymssql.org/){:target="_blank"},
        [mssql](http://www.object-craft.com.au/projects/mssql/){:target="_blank"}.
    9. SAP Sybase:
        [python-sybase](http://python-sybase.sourceforge.net/){:target="_blank"} for SAP Sybase ASE,
        [sqlanydb](https://github.com/sqlanywhere/sqlanydb){:target="_blank"} for Sybase SQL Anywhere.
3. Drivers of Data Warehouse DBs:
    1. Teradata: via ODBC.
4. Driver of [SQLite](https://sqlite.org/){:target="_blank"}: [pysqlite](https://pypi.org/project/pysqlite/){:target="_blank"}.
5. Drivers of Non-relational DBs:
    1. Oracle BerkeleyDB: [bsddb3](https://pypi.org/project/bsddb3/){:target="_blank"}.
    2. Neo4j: [Neo4j Bolt Driver 1.7 for Python](https://neo4j.com/docs/api/python-driver/current/){:target="_blank"}.
6. Drivers of Native Python DBs:
    1. [buzhug](http://buzhug.sourceforge.net/){:target="_blank"} is a fast, portable, pure-Python database engine, using a pythonic non-SQL syntax for all operations.
    2. [SnakeSQL](https://pypi.org/project/SnakeSQL/){:target="_blank"} is a pure Python SQL database written to remove the dependence of the Python Web Modules on 3rd party drivers for non-Python databases like MySQL but designed to be a useful database in its own right.

### MySQL

[MySQL](https://www.mysql.com/){:target="_blank"} is so popular that I don't need to introduce more about it.

Its drivers for Python:
1. [MySQL for Python](https://sourceforge.net/projects/mysql-python/){:target="_blank"}: MySQLdb is a Python DB API-2.0-compliant interface; see [PEP-249](http://www.python.org/peps/pep-0249.html){:target="_blank"} for details.
2. [mysqlclient](https://github.com/PyMySQL/mysqlclient-python){:target="_blank"} is a fork of MySQLdb1.
3. [PyMySQL](http://www.pymysql.org/){:target="_blank"} contains a pure-Python MySQL client library, based on PEP 249.
4. [MySQL Connector/Python](https://dev.mysql.com/downloads/connector/python/){:target="_blank"} is a standardized database driver for Python platforms and development.
5. [mypysql](https://sourceforge.net/projects/mypysql/){:target="_blank"}.

An example of MySQLdb:
```python
#!/usr/bin/env python

import MySQLdb

db = MySQLdb.connect(host="localhost", user="username", passwd="password", db="dbname")
cur = db.cursor()
cur.execute("SHOW TABLES")
for table in cur.fetchall():
    print table[0]
```

### PostgreSQL

[PostgreSQL](https://www.postgresql.org/){:target="_blank"}is a powerful, open source object-relational database system with over 30 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.

Its drivers for Python:
1. [psycopg2](http://initd.org/psycopg/){:target="_blank"} is the most popular PostgreSQL adapter for the Python programming language.
2. [PyGreSQL](http://www.pygresql.org/){:target="_blank"} is an open-source Python module that interfaces to a PostgreSQL database. It embeds the PostgreSQL query library to allow easy use of the powerful PostgreSQL features from a Python script.
3. [pyPgSQL](http://pypgsql.sourceforge.net/){:target="_blank"} is a package of two modules that provide a Python DB-API 2.0 compliant interface to PostgreSQL databases.

An example of psycopg2:
```python
#!/usr/bin/env python

import psycopg2

# Connect to an existing database
conn = psycopg2.connect("host='localhost' dbname='dbname' [user='username' password='password']")
# Open a cursor to perform database operations
cur = conn.cursor()

cur.execute("CREATE TABLE test (id serial PRIMARY KEY, num integer, data varchar);")

cur.execute("SELECT * FROM test;")
cur.fetchone()

# Make the changes to the database persistent
conn.commit()
# Close communication with the database
cur.close()
conn.close()
```

### SQLite

[SQLite](https://sqlite.org/){:target="_blank"} is a C-language library that implements a small, fast, self-contained, high-reliability, full-featured, SQL database engine.

Pros:
- The main engine is written in C, so it should be faster than the gadfly implementation in Python
- It's extensible in a very easy way via Python
- It doesn't put all data in memory like gadfly does (yet you can do that if you want, just use ':memory:' as filename
- It's very cool for small databased application, because you do not have to start an external DBMS
- Implements almost all of SQL92 

Cons:
- SQLite only supports the basic types NULL, INTEGER, FLOAT, TEXT and BLOB
- If you want to use other types like DATE and TIME in pysqlite, you need to use its "pysqlite types mode", where things can get a little nastier. 

pysqlite is an interface to the SQLite 3.x embedded relational database engine. It is almost fully compliant with the Python database API version 2.0 also exposes the unique features of SQLite.

```python
#!/usr/bin/env python

import sqlite3

con = sqlite3.connect("test.db")
con.execute("""CREATE TABLE tbl (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    grp INTEGER)""")
cur = con.cursor()
cur.execute("""INSERT INTO tbl (grp) VALUES (0);""")
newId = cur.lastrowid
print "New rowid =", newId
cur.close()
con.close()
```

### buzhug

[buzhug](http://buzhug.sourceforge.net/){:target="_blank"} is a fast, portable, pure-Python database engine, using a pythonic non-SQL syntax for all operations.

Pros:
- most operations are faster than on other pure-Python databases.
- concurrency control by versioning of records.
- simple system to link databases dynamically (a record of a base can be a field of another base).
- complete documentation .

Cons:
- still beta : bug reports needed.
- no thread-safe feature : should be used behind an asynchronous server for multiple users.

```python
#!/usr/bin/env python

from buzhug import Base
from datetime import date

players = Base("players").create(("name",str),("firstname",unicode),("position",str),("born",date),mode="open")
# p_id = players.insert(column_name="value",...)
# p1 = players.select(name = "value")[0]
# p2 = players[p_id]
# players.update(p1,firstname="value")
```


## References

1. [Python Official Documentation](https://www.python.org/doc/){:target="_blank"}
2. [Web Programming in Python](https://wiki.python.org/moin/WebProgramming){:target="_blank"}
3. [Python Web Development - Python Tutorial](https://pythonspot.com/web-dev/){:target="_blank"}
4. [Python Database - Python Tutorial](https://pythonspot.com/python-database/){:target="_blank"}
