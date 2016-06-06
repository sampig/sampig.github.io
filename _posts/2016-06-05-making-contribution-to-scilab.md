---
layout: post
category : tutorial
tagline: ""
tags : [scilab gerrit]
---
{% include JB/setup %}

This post is to show how to configure ssh and git to get and commit code to Scilab.

### Prequirements

Scilab is using [Git](http://git-scm.com/) to manage the source code. So make sure that you have installed git.

Then you could get the source code from Git:

```
git clone git://git.scilab.org/scilab.git [SCI_GIT_DIR]
```

### 1 Configuration of Gerrit

A valid Scilab's account mail must be provided in order to register on gerrit. [ATOMS](http://atoms.scilab.org/) and [File Exchange](http://fileexchange.scilab.org/) accounts are valid.

To register with gerrit, visit http://codereview.scilab.org/ and log in using your email address and your scilab password.

In order to be able to upload code, you need to create a ssh key that gerrit can use to identify you.

Create a new ssh key if you don't have one:

```
ssh-keygen -t rsa -f ~/.ssh/[PRIVATE_ID_RSA]
```

Log in the gerrit in website, and go to Settings. Paste the _public key_ into the box and click on 'Add' to add the new public key.

To make things easier, set up OpenSSH so that it knows about the defaults for the gerrit server. Edit _~/.ssh/config_, and add a section like:

```
host git.scilab.org
 User [USERNAME]
 IdentityFile ~/.ssh/[PRIVATE_ID_RSA]
 Port 29418
```

(where Username is what you were told on the the 'Profile' page)

You could try to run:

```
ssh git.scilab.org
```

If your name is shown, it works!

### 2 Git

Use the command below to get the source code:

```
git clone ssh://[USERNAME]@git.scilab.org:29418/scilab <name-of-directory>
```

Then you can switch to other branches.

#### 2.1 Configuration

Configure your basic information:

```
git config user.name "John SMITH"
git config user.email "john.smith@scilab.org"
```

You can also use _--global_ parameter to change the global setting for the git.

#### 2.2 Hooks

Some hooks have been set, in order to indent correctly xcos files or to add id-commits when pushing. To set those, in your scilab repository, type the following commands :

```
mv .git/hooks /tmp/
cd .git/
ln -s ../git_hooks/ hooks
```

Git variables settings for XML formatting:

```
git config --global hooks.xmlindent /usr/bin/xmlindent
git config --add xmlindent.ignored 'scilab/Visual-Studio-settings/*.xml' 
git config --add xmlindent.ignored 'scilab/checkstyle/*.xml' 
```

Git variables settings for C/C++ formatting:

```
git config --global hooks.astyle /usr/bin/astyle
git config --add astyle.ignored 'scilab/modules/*/src/jni/*.hxx'
git config --add astyle.ignored 'scilab/modules/*/src/jni/*.cpp'
git config --add astyle.ignored 'scilab/modules/javasci/src/java/org/scilab/modules/javasci/Call_Scilab*.java'
git config --add astyle.ignored 'scilab/modules/helptools/src/java/org/scilab/modules/helptools/SynopsisLexer.java'
git config --add astyle.ignored 'scilab/modules/helptools/src/java/org/scilab/modules/helptools/XML/XMLLexer.java'
git config --add astyle.ignored 'scilab/modules/helptools/src/java/org/scilab/modules/helptools/c/CLexer.java'
git config --add astyle.ignored 'scilab/modules/helptools/src/java/org/scilab/modules/helptools/java/JavaLexer.java'
git config --add astyle.ignored 'scilab/modules/helptools/src/java/org/scilab/modules/helptools/scilab/ScilabLexer.java'
git config --add astyle.ignored 'scilab/modules/scinotes/src/java/org/scilab/modules/scinotes/FunctionScanner.java'
git config --add astyle.ignored 'scilab/modules/scinotes/src/java/org/scilab/modules/scinotes/IndentScanner.java'
git config --add astyle.ignored 'scilab/modules/scinotes/src/java/org/scilab/modules/scinotes/MatchingBlockScanner.java'
git config --add astyle.ignored 'scilab/modules/scinotes/src/java/org/scilab/modules/scinotes/ScilabLexer.java'
git config --add astyle.ignored 'scilab/modules/scicos/src/scicos_sundials/*'
```

After that, you could try to view _.git/config_ where you can find your changes for the configuration of git in this project.

### References

1. [Scilab Code Review](https://codereview.scilab.org/)
2. [Git and Gerrit CodeReview for Scilab developpers](https://wiki.scilab.org/gerrit)
3. [Using Git to contribute code to Scilab](https://wiki.scilab.org/GIT)
4. [Scilab - ATOMS](http://atoms.scilab.org/)
5. [Scilab - File Exchange](http://fileexchange.scilab.org/)
