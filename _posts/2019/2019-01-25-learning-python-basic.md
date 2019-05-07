---
layout: post
title: "Learning Python: Basic"
date: 2019-01-25 15:00:00 +0100
category: tutorial
tagline: ""
tags: [Python]
abstract : "Learn some basic and useful usage of Python. This is just a learning note of mine own."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Special Comment](#special-comment)
* [Data Structures](#data-structures)
    * [List Object](#list-object)
    * [Tuples and Sequences](#tuples-and-sequences)
    * [Sets](#sets)
    * [Dictionaries](#dictionaries)
    * [Looping Through Sequences](#looping-through-sequences)
* [Modules](#modules)
* [Mathematical](#mathematical)
    * [Generate pseudo-random numbers](#generate-pseudo-random-numbers)
* [Input and Output](#input-and-output)
    * [Output Formatting](#output-formatting)
    * [Reading and Writing Files](#reading-and-writing-files)
* [Classes and Objects](#classes-and-objects)
    * [Classes](#classes)
    * [Inheritance](#inheritance)
    * [Inner Classes](#inner-classes)
    * [Static Methods](#static-methods)
* [Recursion Control](#recursion-control)
* [Logging](#logging)
    * [Logging Configuration](#logging-configuration)
    * [Logging Formatter](#logging-formatter)
* [Subprocess Management](#subprocess-management)
    * [Using the subprocess Module](#using-the-subprocess-module)
    * [Popen Constructor](#popen-constructor)
* [Threads Management](#threads-management)
    * [Lower Level Interfaces](#lower-level-interfaces)
    * [Higher Level Interfaces](#higher-level-interfaces)
    * [multiprocessing](#multiprocessing)
* [Lambda Expressions](#lambda-expressions)
* [References](#references)


## Introduction

Python is more and more popular. It is widely used, such as for desktop applications, web applications, data science and so on.

In this blog, there are only some basic knowledges about Python. Codes might be run in Python 2.7 or 3.x.
More examples can be found in my GitHub project - [ZhuzhuLearning](https://github.com/sampig/ZhuzhuLearning/Python/basic){:target="_blank"}.


## Special Comment

Sometimes, there are comments in the first line or the first two lines.

If you want to make Python scripts directly executable on BSD'ish Unix systems, you could put a UNIX “shebang” line at the beginning and give the file an executable mode.
This line should also be the first line. The syntax is as follows:

```python
#!/usr/bin/env python
```

By default, Python source files are treated as encoded in ASCII.
You can declare another encoding with a special comment. The syntax is as follows:

```python
# -*- coding: encoding -*-
```


## Data Structures

### List Object

#### Built-in Methods on Lists

The _list_ data type has some built-in methods:
- list.append(x) equivalent to a[len(a):] = [x]
- list.extend(L) equivalent to a[len(a):] = L
- list.insert(i, x)
- list.remove(x)
- list.pop([i])
- list.index(x)
- list.count(x)
- list.sort(cmp=None, key=None, reverse=False)
- list.reverse()

#### Use Lists as Stacks or Queues

Stack: last-in, first-out.
Use __append()__ to add an item to the top of the stack and use ___pop()__ to retrieve an item from the top of the stack.

Queue: first-in, first-out.
Lists are not efficient for this purpose. But we could use __collections.deque__ to implement a queue. Use __popleft()__ to retrieve the first item in the queue.

#### Functional Programming Tools

```filter(function, sequence)``` returns a sequence consisting of those items from the sequence for which ```function(item)``` is true.

```map(function, sequence)``` calls ```function(item)``` for each of the sequence's items and returns a list of the return values.
More than one sequence could be the parameters.

```reduce(function, sequence)``` returns a single value constructed by calling the binary function ```function()``` on the first two items of the sequence, then on the result and the next item.

#### List Comprehensions

List comprehensions provide a concise way to create lists.
Some examples:

```python
squares = [x**2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
[(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
# [(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]

[[row[i] for row in matrix] for i in range(4)]
# [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

#### Remove Items in List

The __del__ statement can be used to remove slices from a list or to delete entire variables.

### Tuples and Sequences

#### Sequences

In Python 2.7, there are seven sequence types: strings, Unicode strings, lists, tuples, byte-arrays, buffers and xrange objects.

In Python 3.x, there are five sequence types: lists, tuples and range objects are basic; binary data and text strings are additional.

Their detailed introduction and operations could be found in [Sequence Types in Python 2.7 Documentation](https://docs.python.org/2/library/stdtypes.html#typesseq){:target="_blank"} and [Sequence Types in Python 3.7 Documentation](https://docs.python.org/3/library/stdtypes.html#typesseq){:target="_blank"}.

#### Tuples

A tuple consists of a number of values separated by commas.
Different from lists, tuples are immutable and can contain a heterogeneous sequence of elements that are accessed via unpacking or indexing.
Even though tuples are immutable, but they can contain mutable objects.

```python
t = 123, "asdf", [1, 2, 3]
```

An empty tuple is constructed by an empty pair of parentheses and a tuple with one item is constructed by following a value with a comma.

```python
empty_tuple = ()
single_tuple = "single", 
```

The statement ```t = 123, "asdf", [1, 2, 3]``` is an example of tuple packing. The reverse operation is also possible: ```x, y, z = t```, called sequence unpacking.

### Sets

A set is an unordered collection with no duplicate elements.
Curly braces `{}` or the `set()` function can be used to create sets. However, use `set()` to create an empty set instead of `{}`.

Set objects support mathematical operations like union `a | b`, intersection `a & b`, difference `a - b` and symmetric difference `a ^ b`.

### Dictionaries

Dictionaries are mapping types. A dictionary is like a set of `key: value` pairs, with the requirement that the keys are unique but must be an immutable type (tuples that contain only strings, numbers or tuples can also be used as keys).
Use a pair of braces `{}` to create an empty dictionary.

The main operations on a dictionary are storing a value with some keys and extracting the value given the key. Other operations:
- Delete a `key: value` pair with `del`.
- In Python 2.7, the `.keys()` method of a dictionary object returns a list of all the keys used in the dictionary. In Python 3.x, the `list(d)` method on a dictionary returns a list of all the keys.
- To check whether a single key is in the dictionary, use the `in` keyword.

The `dict()` constructor builds dictionaries directly from sequences of key-value pairs:

```python
d1 = dict([('a', 1), ('b', 2), ('c', 3)])
d2 = dict(a = 1, b = 2, c = 3)
```

### Looping Through Sequences

In both Python 2.7 and 3.x, use `enumerate()` function to loop through a _sequence_ with the position index and corresponding value.

```python
for i, v in enumerate(s):
    print(i, v)
```

However, use `.iteritems()` method in Python 2.7 or use `.items()` method in Python 3.x, to loop through a _dictionary_ with the key and corresponding value.

To loop over two or more sequences at the same time, the entries can be paired with the `zip()` function.

```python
for item1, item2 in zip(s1, s2):
    print(item1, item2)
```

To loop over a sequence in reverse, use the `reversed()` function.

It is not recommended to change a list while looping over it. It is often simpler and safer to create a new list instead.


## Modules

A module is a Python file (*.py) containing executable statements and function definitions.
Use the `import` statement to import a module or the `from ? import ?` to import the symbol in a module.

A compiled Python file (*.pyc) is automatically generated to speed up the module loading according to the original module file.
More details about compiled Python files can be found in [6.1.3. “Compiled” Python files for Python 2.x](https://docs.python.org/2/tutorial/modules.html#compiled-python-files){:target="_blank"} and [6.1.3. “Compiled” Python files for Python 3.x](https://docs.python.org/3/tutorial/modules.html#compiled-python-files){:target="_blank"}

When a module is imported, the Python interpreter first searches for a built-in module with that name. If not found , it then searches for the file with that name in a list of directories given by the variable `sys.path` (it is a list of strings that specifies the search path for modules). A program is free to modify this path list for its own purposes.

The built-in function `dir()` is used to find out which names a module defines:
```python
import __builtin__, sys
dir(__builtin__)
dir(sys)
```

Packages are a way of structuring Python's module namespace by using "dotted module names".
A `__init__.py` file is required to make Python treats this directory as a containing package.
We could also use the `from ? import ?` to import from packages.


## Mathematical

Python provides some modules about numeric and mathematical functions and data types, such as __numbers__, __math__, __cmath__, __decimal__, __fractions__, __random__, __operator__.

### Generate pseudo-random numbers

The `random` module implements pseudo-random number generators for various distributions.

Python uses the Mersenne Twister as the core generator. It produces 53-bit precision floats and has a period of 2<sup>19937</sup>-1

```python
#!/usr/bin/env python2.7
import random

# Generate a random float between 0.0 and 1.0 (0.0 <= x < 1.0)
print random.random()

# Generate a random integer from 1 to 100 (1 <= x <= 100)
print random.randint(1, 100)

# Generate a random float between 1.0 and 10.0 (1.0 <= x < 10.0)
print random.uniform(1, 10)

# Generate an even interger from 0 to 100
print random.randrange(0, 101, 2)

# Choose a random element
random.choice("abcdefghij")

# Shuffle a list
items = [1, 2, 3, 4, 5]
random.shuffle(items)
print items

# Choose random items from a list
languages = ["Python", "Java", "SQL", "C", "JavaScript"]
lang = random.sample(languages, 3)
print lang
```


## Input and Output

There are several ways to read the input and present the output of a program.

### Output Formatting

Two functions `repr()` and `str()` provided by Python can be used to convert values to strings.
The `str()` function is meant to return representations of values which are fairly human-readable, while `repr()` is meant to generate representations which can be read by the interpreter.

```python
#!/usr/bin/env python2.7

s = "string\n"
print s
print str(s)
print repr(s)
```

There are two ways to format the output: the first way is to do all the string handling using string slicing and concatenation operations; the second way is to use the `str.format()`, `str.rjust()`, `str.ljust()`, `str.center()`, `str.zfill()` methods.

```python
#!/usr/bin/env python2.7

for x in range(1, 25, 5):
    print "{0:3d}, {1:5d}".format(x * x, x * x * x)

for x in range(1, 25, 5):
    print str(x * x * x).rjust(5), str(x * x).ljust(5)

print "12".zfill(5)
print "-3.14".zfill(7)
```

Other usage of the `str.format()` method are like:

```python
#!/usr/bin/env python2.7

print "Empty: {} and {}.".format("param1", "param2")

print "Position numbers: {1}, {2} and {0}.".format("param1", "param2", "param3")

print "Name values: {one} and {two}.".format(one="param1", two="param2")
```

'`!s`' (apply `str()`) and '`!r`' (apply `repr()`) can be used to convert the value before it is formatted.

```python
#!/usr/bin/env python2.7

import math
print "The value of PI is approximately {!r}.".format(math.pi)
```

An optional '`:`' and format specifier can follow the field name.

```python
#!/usr/bin/env python2.7

import math

print "The value of PI is approximately {0:.3f}.".format(math.pi)

dict = {"Value1": 123, "Value2": 345}
for k, v in dict.items():
    print "{0:10} ==> {1:10d}".format(k, v)

# other usage:
print "V1: {0[Value1]:d}".format(dict)
print "V2: {Value2:d}".format(**dict)
```

In Python 3.6+, Formatted string literals (also called f-strings for short) could be used for the Python expressions by prefixing the strings with `f` or `F` and writing expressions as `{expression}`.

```python
#!/usr/bin/env python3.7

import math
print(f'The value of pi is approximately {math.pi:.3f}.')
```

The `%` operator can also be used for string formatting.

### Reading and Writing Files

`open(filename[, mode[, buffering[, ...]]])` returns a file object.
The available modes are:

| Character | Meaning |
|-----------|---------|
| 'r'       | open for reading (default) |
| 'w'       | open for writing, truncating the file first |
| 'x'       | open for exclusive creation, failing if the file already exists |
| 'a'       | open for writing, appending to the end of the file if it exists |
| 'b'       | binary mode |
| 't'       | text mode (default) |
| '+'       | open a disk file for updating (reading and writing) |

Binary files are buffered in fixed-size chunks (`io.DEFAULT_BUFFER_SIZE`). On many systems, the buffer will typically be 4096 or 8192 bytes long.

`f.read([size])` is used to read a file's contents.
If the end of the file has been reached, `f.read()` will return an empty string ("").

`f.readline()` reads a single line from the file; a newline character (`\n`) is left at the end of the string.
For reading lines from a file, you can loop over the file object. This is memory efficient, fast, and simple.

`list(f)` and `f.readlines()` can be used to read all the lines in a file.

`f.write(string)` writes the contents of string to the file, returning `None`.

`f.tell()` returns an integer giving the file object's current position in the file, measured in bytes from the beginning of the file.

`f.seek(offset, from_what)` is used to change the file object's position. (A `from_what` value of 0 measures from the beginning of the file, 1 uses the current file position, and 2 uses the end of the file as the reference point.)

`f.close()` is used to close a file and to free up any system resources taken up by the open file.


## Classes and Objects

### Classes

Python classes provide all the standard features of Object Oriented Programming: the class inheritance mechanism allows multiple base classes, a derived class can override any methods of its base class or classes, and a method can call the method of a base class with the same name.

A Python class also have the instantiation (to create a new instance of the class) and two attribute references (attributes and methods).
When involving mutable objects such as lists and dictionaries, the attributes have some different properties: they will share data among instances.

An example of class:
```python
#!/usr/bin/env python2.7

class Player(object):
    """A Player class"""
    numbers = []
    def __init__(self, name=None):
        if name is not None:
            self.name = name
    def print_numbers(self):
        print self.name, "numbers:", self.numbers

# the docstring belonging to the class:
print Player.__doc__

p1 = Player("P1")
p2 = Player("P2")
p1.numbers.append(1)
p1.print_numbers()
p2.print_numbers()
p2.numbers.append(2)
p1.print_numbers()
p2.print_numbers()
p1.numbers = []
p1.numbers.append(3)
p2.numbers.append(4)
p1.print_numbers()
p2.print_numbers()
```

Other features:
1. Method overloading.
2. Encapsulation(private methods and variables).
Private methods and variables start with two underscores and are accessible only in their own class. However, it is a trick that the methods can still be invoked by using `_classname__method()`.
3. Polymorphism.

### Inheritance

The syntax for a derived class definition looks like `class DerivedClassName(BaseClassName)`.

- `isinstance(object, classinfo)` is used to check an instance's type. Return true if the _object_ argument is an instance of the _classinfo_ argument, or of a (direct, indirect or virtual) subclass thereof.
- `issubclass(class, classinfo)` is used to check class inheritance. Return true if _class_ is a subclass (direct, indirect or virtual) of _classinfo_.

Python supports multiple inheritance, like `class DerivedClassName(Base1, Base2, Base3)`.
The ordering of the classes is dynamic. More details can be found in [The Python 2.3 Method Resolution Order](https://www.python.org/download/releases/2.3/mro/){:target="_blank"}

### Inner Classes

It is possible to create an inner class. An inner class is defined entirely in the body of the outer class.

```python
#!/usr/bin/env python2.7

class OuterClass:
    class InnerClass:
        pass
```

### Static Methods

If you want to create a static method, use `variable_name = staticmethod(method_name)`.

```python
#!/usr/bin/env python2.7

class ClassStatic:
    def static_method():
        print "This could be a static method."
    invoke_name = staticmethod(static_method)

ClassStatic.invoke_name()
```


## Recursion Control

Recursive functions are useful in programming. Since the function is recursive, calling itself and storing some memory, it could cost much more memory than expected.
In Python, we could use `sys.setrecursionlimit()` to stop the function after the depth of the limitation.

```python
#!/usr/bin/env python2.7

import sys

sys.setrecursionlimit(50)

def add_up(num):
    if num == 1:
        return 1
    else:
        return num + add_up(num - 1)

print add_up(3)
try:
    print add_up(50)
except Exception, e:
    print e
```


## Logging

In Python, the _logging_ module provides some functions for logging: `debug()`, `info()`, `warning()`, `error()` and `critical()`, which are named after the level of severity of the events.
The level or severity of logging importance are:

| Level | Description |
|-------|-------------|
| DEGUG    | Detailed information for diagnosing problems. |
| INFO     | Confirmation for expected work. |
| WARNING  | An indication that something unexpected happened. |
| ERROR    | A more serious problem that some functions are not able to work. |
| CRITICAL | A serious error. |

Use `logging.basicConfig()` to configure the logging. Some of its arguments are:

| Format | Description |
|--------|-------------|
| filename | Specifies that a FileHandler be created, using the specified filename, rather than a StreamHandler. |
| filemode | If filename is specified, open the file in this mode. Defaults to 'a'. |
| format   | Use the specified format string for the handler. |
| datefmt  | Use the specified date/time format, as accepted by `time.strftime()`. |
| level    | Set the root logger level to the specified level. |

The numeric values of logging levels are: CRITICAL(50), ERROR(40), WARNING(30), INFO(20), DEBUG(10) and NOTSET(0). We could even define our own levels.

```python
#!/usr/bin/env python2.7

import logging

output_format = "%(asctime)s %(levelname)s\t%(module)s %(funcName)s %(lineno)d %(message)s"
# logging.basicConfig(filename="program.log",level=logging.DEBUG)
logging.basicConfig(format=output_format, level=logging.DEBUG)
logging.debug("Debug message.")
logging.info("Info message.")
logging.warning("Warning message.")
```

### Logging Configuration

There are 3 ways to configure logging:
1. create loggers, handlers and formatters in codes.
2. create a logging config file and use `fileConfig()` function.
3. create a dictionary of configuration information and use `dictConfig()` function.

```python
#!/usr/bin/env python2.7

import logging

# create logger
logger = logging.getLogger("simple_example")
logger.setLevel(logging.DEBUG)

# create console handler and set level to debug
ch = logging.StreamHandler()
ch.setLevel(logging.DEBUG)

# create formatter
formatter = logging.Formatter("%(asctime)s - %(name)s - %(levelname)s - %(message)s")

# add formatter to ch
ch.setFormatter(formatter)

# add ch to logger
logger.addHandler(ch)
```

```python
#!/usr/bin/env python2.7

import logging
import logging.config

logging.config.fileConfig("logging.conf")

# create logger
logger = logging.getLogger("simpleExample")
```

In the _logging.conf_ file:

```
[loggers]
keys=root,simpleExample

[handlers]
keys=consoleHandler

[formatters]
keys=simpleFormatter

[logger_root]
level=DEBUG
handlers=consoleHandler

[logger_simpleExample]
level=DEBUG
handlers=consoleHandler
qualname=simpleExample
propagate=0

[handler_consoleHandler]
class=StreamHandler
level=DEBUG
formatter=simpleFormatter
args=(sys.stdout,)

[formatter_simpleFormatter]
format=%(asctime)s - %(name)s - %(levelname)s - %(message)s
datefmt=
```

### Logging Formatter

`%(<dictionary key>)s` are used to format the message style; the possible keys are:

| Key | Format | Description |
|-----|--------|-------------|
| asctime   | %(asctime)s   | Human-readable time when the LogRecord was created. |
| filename  | %(filename)s  | Filename portion of pathname. |
| funcName  | %(funcName)s  | Name of function containing the logging call. |
| levelname | %(levelname)s | Text logging level for the message ('DEBUG', 'INFO', 'WARNING', 'ERROR', 'CRITICAL'). |
| lineno    | %(lineno)d    | Source line number where the logging call was issued (if available). |
| module    | %(module)s    | Module (name portion of filename). |
| message   | %(message)s   | The logged message, computed as msg % args. This is set when Formatter.format() is invoked. |

More details can be found in [LogRecord attributes in Python 2.7](https://docs.python.org/2/library/logging.html#logrecord-attributes){:target="_blank"} and [LogRecord attributes in Python 3.7](https://docs.python.org/3/library/logging.html#logrecord-attributes){:target="_blank"}.


## Subprocess Management

### Using the subprocess Module

The _subprocess_ module allows to spawn new processes, connect to input/output/error pipes, and obtain return codes. There are some convenience functions to launch subprocesses:

1. `subprocess.call(args, *, stdin=None, stdout=None, stderr=None, shell=False)`
2. `subprocess.check_call(args, *, stdin=None, stdout=None, stderr=None, shell=False)`
3. `subprocess.check_output(args, *, stdin=None, stderr=None, shell=False, universal_newlines=False)`<br/>
Run command with arguments and return its output as a byte string.
4. `subprocess.run(args, *, stdin=None, input=None, stdout=None, stderr=None, capture_output=False, shell=False, cwd=None, timeout=None, check=False, encoding=None, errors=None, text=None, env=None, universal_newlines=None)`<br/>
This function is new in Python 3.5.

> The usage of `shell=True` should be very careful. The detailed reasons and explanation can be found in [Subprocess - Frequently Used Arguments in Python 2.7](https://docs.python.org/2/library/subprocess.html#frequently-used-arguments){:target="_blank"} and [Subprocess - Security Considerations in Python 3.7](https://docs.python.org/3/library/subprocess.html#security-considerations){:target="_blank"}.

```python
#!/usr/bin/env python2.7

import subprocess

subprocess.call(["ls", "-l"])

s = subprocess.check_output(["ping", "-c 1", "www.google.com"])
print "s =", str(s)
```

```python
#!/usr/bin/env python3

import subprocess

subprocess.run(["ls", "-l"])

s = subprocess.run(["ping", "-c 1", "www.google.com"], check =True, stdout=subprocess.PIPE).stdout
print("s = " + s.decode())
```

### Popen Constructor

The _Popen_ class in _subprocess_ module deals with the creation and management of the process.

`class subprocess.Popen(args, bufsize=0, executable=None, stdin=None, stdout=None, stderr=None, preexec_fn=None, close_fds=False, shell=False, cwd=None, env=None, universal_newlines=False, startupinfo=None, creationflags=0)` (Python 2.7)

Use `Popen.communicate(input=None)` to interact with process. Send data to stdin and it returns a tuple `(stdoutdata, stderrdata)`. Popen objects have other methods: `poll()`, `wait()`, `send_signal(signal)`, `terminate()` and `kill()`.

```python
#!/usr/bin/env python2.7

import subprocess

process = subprocess.Popen(["ping", "-c 1", "www.google.com"], stdout=subprocess.PIPE, stderr=subprocess.PIPE)
stdout, stderr = process.communicate()
print stdout
```


## Threads Management

A thread is the smallest sequence of programmed instructions. A process can contains more than one thread. Threads in a process share memory and resources.

Python provides some modules for threads management.

### Lower Level Interfaces

In Python 2.x, the __thread__ module provides low-level primitives for working with multiple threads.

In Python 3.x, the module changes to ___thread__.

### Higher Level Interfaces

Python also provides a higher-level threading interfaces, called __threading__ module. Some important classes or objects in this module:

1. `class threading.Thread(group=None, target=None, name=None, args=(), kwargs={}, *, daemon=None)`<br/>
This class represents an activity that is run in a separate thread of control. There are two ways to specify the activity: by passing a callable object to the constructor or by overriding the `run()` method in a subclass.<br/>
Once a thread object is created, its activity must be started by calling the thread's `start()` method. This invokes the run() method in a separate thread of control.
2. `class threading.Timer(interval, function, args=[], kwargs={})`
This class represents an action that should be run only after a certain amount of time has passed -- a timer.
3. A primitive lock is a synchronization primitive that is not owned by a particular thread when locked. 
Use `threading.Lock()` this factory function to get a new primitive lock object.

```python
#!/usr/bin/env python2.7

import threading
import time
from threading import Timer

# Create a new thread class
class NewThread(threading.Thread):
    
    def __init__(self, name):
        threading.Thread.__init__(self)
        self.name = name

    def run(self):
        print "Thread -", self.name, "is running."


def startRunning():
    while(True):
        print "Keep running..."
        time.sleep(5)


# Use a Timer
t2 = Timer(5.0, startRunning)
t1 = NewThread("ZZ Thread")
t2.start()
t1.start()
```

### multiprocessing

__multiprocessing__ is a package that supports spawning processes using an API similar to the __threading__ module.
It offers both local and remote concurrency, effectively side-stepping the Global Interpreter Lock by using subprocesses instead of threads.


## Lambda Expressions

One use of lambda expression is to create anonymous functions, and the other use of it is to pass a small function as an argument.

> lambda_expr     ::=  "lambda" [parameter_list]: expression

The unnamed function object behaves like a function object defined with:

```
def <lambda>(parameters):
    return expression
```

Functions created with lambda expressions cannot contain statements.

Some examples:

```python
#!/usr/bin/env python2.7
f = lambda x : x * x
print f(5)
# 25
```

```python
#!/usr/bin/env python2.7
def my_lambda_func(p):
    return lambda p1, p2: (p1 + p2) * p

f = my_lambda_func(5)
print f(2, 3)
# 25
```

```python
#!/usr/bin/env python2.7
pairs = [(1, "one"), (2, "two"), (3, "three"), (4, "four")]
pairs.sort(key=lambda pair: pair[1])
print pairs
# [(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]

arr = [1, 2, 3, 4, 5]
squaredArray = map(lambda x: x * x, arr)
print squaredArray
# [1, 4, 9, 16, 25]

filterArray = filter(lambda x: x % 2 == 0, arr)
print filterArray
# [2, 4]

reduceArray = reduce(lambda x, y: x + y,  arr)
print reduceArray
# 15
```


## References

1. [Python Official Documentation](https://www.python.org/doc/){:target="_blank"}
2. [Python 2.7.16 documentation](https://docs.python.org/2/index.html){:target="_blank"}
3. [Python 3.7.2 documentation](https://docs.python.org/3/index.html){:target="_blank"}
