---
layout: post
title: "Learning Python: GUI"
date: 2019-01-27 15:00:00 +0100
category: tutorial
tagline: ""
tags: [Python]
abstract : "Learning Note: using some modules such as PyQt and Tk to develop Python GUI applications."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Tkinter](#tkinter)
* [PyQt](#pyqt)
* [wxWidgets](#wxwidgets)
* [References](#references)


## Introduction

There are several platform-independent GUI toolkits for Python: [Tkinter](https://www.tcl.tk/){:target="_blank"}, [PyQt](https://riverbankcomputing.com/software/pyqt/intro){:target="_blank"}, [wxWidgets](https://www.wxwidgets.org/){:target="_blank"}, [Gtk+](https://www.gtk.org/){:target="_blank"}, [FLTK](https://www.fltk.org/){:target="_blank"} and [PyOpenGL](http://pyopengl.sourceforge.net/){:target="_blank"}.


## Tkinter

[Tkinter](https://www.tcl.tk/){:target="_blank"} is the standard GUI package for Python.
Tk is a graphical user interface toolkit that takes developing desktop applications to a higher level than conventional approaches. Tk is the standard GUI not only for Tcl, but for many other dynamic languages, and can produce rich, native applications that run unchanged across Windows, Mac OS X, Linux and more.

```python
#!/usr/bin/env python

import Tkinter

master = Tkinter.Tk()
Tkinter.mainloop()
```

Some widgets of Tkinter: buttons, labels, check buttons, radio buttons, list box, scroll box, progress bar and a few others.


## PyQt

[PyQt](https://riverbankcomputing.com/software/pyqt/intro){:target="_blank"} is a set of Python v2 and v3 bindings for Qt application framework. PyQt combines all the advantages of Qt and Python.

>  PyQt4 and Qt v4 are no longer supported and no new releases will be made. PyQt5 and Qt v5 are strongly recommended for all new development. 

```python
#!/usr/bin/env python

import sys
from PyQt5.QtWidgets import QApplication, QMainWindow

app = QApplication(sys.argv)
main = QMainWindow()
main.setWindowTitle("Zhuzhu PyQt5")
main.show()
sys.exit(app.exec_())
```

Some widgets of PyQt: window, buttons, message boxes, text boxes, menus, tables, tabs, layouts, dialogs, progress bar and a few others.


## wxWidgets

[wxWidgets](https://www.wxwidgets.org/){:target="_blank"} is a free, portable GUI class library written in C++ that provides a native look on a number of platforms. Language bindings are available for many languages including Python.

[wxPython](https://www.wxpython.org/){:target="_blank"} is the Python binding for wxWidgets. It can be used to create Python GUI. Unlike Qt or Tk which have a custom Qr or Tk look, applications made with wxPython have a native appearance on all platforms.

A simple example:
```python
#!/usr/bin/env python

import wx

app = wx.App(False)
frame = wx.Frame(None, wx.ID_ANY, "Hello World")
frame.Show(True)
app.MainLoop()
```

Some widgets of wxPython: window, buttons, dialogs, input field, menu and tabs.


## References

1. [Python Official Documentation](https://www.python.org/doc/){:target="_blank"}
2. [Python 2.7.16 documentation](https://docs.python.org/2/index.html){:target="_blank"}
3. [Python 3.7.2 documentation](https://docs.python.org/3/index.html){:target="_blank"}
4. [Tkinter](https://www.tcl.tk/){:target="_blank"}
5. [PyQt](https://riverbankcomputing.com/software/pyqt/intro){:target="_blank"}
6. [wxWidgets](https://www.wxwidgets.org/){:target="_blank"}
7. [wxPython](https://www.wxpython.org/){:target="_blank"}
8. [Examples in my GitHub](https://github.com/sampig/ZhuzhuLearning/Python/gui){:target="_blank"}
