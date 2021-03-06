---
layout: post
title: "Building YUI"
date: 2020-09-06 11:15:00 +0200
category: tutorial
tagline: ""
tags: [JavaScript, YUI]
abstract : "Learning YUI: building YUI library and its documentation."
---
{% include JB/setup %}

* [Background](#background)
* [Build YUI](#build-yui)
  - [Preparation](#preparation)
  - [Building Steps](#building-steps)
  - [Bugs Fix](#bugs-fix)
  - [Using YUIDoc](#using-yuidoc)
* [Alternatives](#alternatives)
* [References](#references)


# Background

The official website of [YUI](http://yuilibrary.com/){:target="_blank"} is not available and it might not be coming back. Here are some alternatives.


# Build YUI

## Preparation

Install Node.js and other tools globally:

```bash
npm -g install grunt-cli
npm -g install shifter
npm -g install yogi
npm -g install phantomjs
```

## Building Steps

Get the source from git.

```bash
git clone https://github.com/yui/yui3.git
```

Install required modules locally. Sometimes some modules failed to install. If so, then install them one by one.

```bash
npm install
 
npm install grunt
```

One of the commands below can be used to build the library:

```bash
grunt release
 
grunt build
 
yogi build
 
cd src && shifter --walk
```

The first one `grunt release` will create _release_ directory. This directory contains the few kinds of builds in which YUI deploys.

The third one `yogi build` just builds the tree.

The second one `grunt build` runs `yogi build` and `npm i`.

The last one `shifter` is used to rebuild the entire YUI _src_ tree.

## Bugs Fix

### Errors

There are some errors while building in my machine.

__1. error in cpr module.__

```
Running "npm-copy" task
Copying to build dir: /usr/local/www/static/vendor/yui3/build-npm
**Fatal error: Path must be a string. Received undefined**
```

This is caused by `cpr` module (it could be in _node_modules_ or _node_modules/grunt-yui-contrib/node_modules_).

Modify the `createFiles` function in the _cpr/lib/index.js_:

```js
var from = files.pop(),
    to = options.toHash[from];
if (!from) {
    return check();
}
var dir = path.dirname(to);
```

__2. error in yogi about grover module.__

```
yogi [bail] grover is not installed :(
Fatal error: yogi test exited with code: 1
```

Copy the _grover_ module into _yogi_ module:

```bash
cp -R node_modules/grover node_modules/yogi/node_modules/
```

__3. error in yuitest module.__

Two different errors related to `yuitest`:

```
Found a local install of YUITest, remove it please..

local yogi yuitest can not be found, you may need to reinstall yogi..
```

Remove the `yuitest` in _node_modules/.bin_ and create a symbol link for `yuitest` in _node_modules/yogi/node_modules/.bin_.

```bash
rm node_modules/.bin/yuitest
 
cd node_modules/yogi/node_modules/.bin
ln -s ../../../yuitest/cli.js yuitest
```

__4. error in unit test.__

In _src/yql/tests/unit/assets/yql-tests.js_, all the unit tests such as `test_query`, `test_https` and so on are failing.

The API from Yahoo (http://query.yahooapis.com/v1/public/yql) is not available anymore. So, the query with the YQLRequest object cannot succeed.

We can delete those testings.

In _src/yui/tests/unit/assets/object-test.js_, one assert is incorrect:

```js
Assert.areSame(0, Y.Object.size('foo'));
```

The value should be 3.

### Results

Unfortunately, I cannot build the library successfully yet after all these modifications.

The building process is stuck in:

```
yogi [info] yuitest tests complete
Starting Grover on 302 files with PhantomJS@2.1.1
Running 15 concurrent tests at a time.
Using a 120 second timeout per test.
```

It cannot continue. The release directory is not generated. But a directory named _build-npm_ is generated.

## Using YUIDoc

We can also use YUIDoc to generate API docs for YUI.

Create a yuidoc.json file like:

```js
{
    "name": "YUI API documentation version",
    "description": "YUI API documentation generated by YUIDoc",
    "version": "3.18.1",
    "url": "https://github.com/yui/yui3",
    "options": {
        "linkNatives": "true",
        "outdir": "./api",
        "paths": "."
    }
}
```

`outdir` is output directory and `paths` is directory of the library.

Generate the documentation or run it as a server:

```bash
yuidoc .
 
yuidoc . --server [port]
```

After this, the API documentation in HTML format are generated in the output directory.

![API dirs]({{ site.url }}/assets/images/building_yui/api_dir.png)

![API pages]({{ site.url }}/assets/images/building_yui/api_page.png){:width="600px"}

# Alternatives

Other alternatives online:

1. [http://yssl.org/lib/yui/docs/](http://yssl.org/lib/yui/docs/){:target="_blank"}
2. [http://yssl.org/lib/yui/api/](http://yssl.org/lib/yui/api/){:target="_blank"}
3. [https://web.archive.org/web/20140902233923/http://www.yuilibrary.com/](https://web.archive.org/web/20140902233923/http://www.yuilibrary.com/){:target="_blank"}


# References

1. [YUI 3: The Yahoo User Interface Library at GitHub](https://github.com/yui/yui3){:target="_blank"}
2. [YUIDoc:  YUI Javascript Documentation Tool at GitHub](https://github.com/yui/yuidoc){:target="_blank"}
3. [YUI Developer Workflow](https://github.com/yui/yui3/wiki/Developer-Workflow#building-yui){:target="_blank"}
4. [Using YUIDoc](http://yui.github.io/yuidoc/args/index.html){:target="_blank"}
