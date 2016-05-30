---
layout: post
category : tutorial
tagline: ""
tags : [scilab]
---
{% include JB/setup %}

This post is to show how to compile Scilab in Ubuntu 16.04 from my experience. (Ignore what is not working on your environment.)

### Prequirements

Scilab is using [Git](http://git-scm.com/) to manage the source code and the dependencies are managed on [Subversion](http://subversion.apache.org/) as per platform binary libraries. So make sure that you have installed git and subversion.

### 1 Get Sources of Scilab

Get the source code from Git:

```
git clone -b master --depth=1 git://git.scilab.org/scilab.git [SCI_GIT_DIR]
```

Or when you have an account in Scilab: 

```
git clone -b master ssh://[USERNAME]@git.scilab.org:29418/scilab.git [SCI_GIT_DIR]
```

Then get the libraries of dependencies from subversion:

```
svn --force checkout --username anonymous --password Scilab svn://svn.scilab.org/scilab/trunk/Dev-Tools/SE/Prerequirements/[linux_x64 | linux]/ [SCI_GIT_DIR]/scilab/
```


### 2 Install some other Dependencies

Install gfortran, g++, ocaml-nox, libgl1-mesa-dev, libtool and automake (if there were some problems when running './configure'):

```
sudo apt-get install gfortran
sudo apt-get install g++
sudo apt-get install ocaml-nox
sudo apt-get install libgl1-mesa-dev
sudo apt-get install libtool
sudo apt-get install automake
```

Install OracleJDK instead of OpenJDK. There are many ways to install JDK.

1. Update apt repository to install:

```
sudo add-apt-repository ppa:webupd8team/java
sudo apt update
sudo apt install oracle-java8-installer
```

2. Download the binaries from the official website and configure it.

```
sudo update-alternatives --install /usr/bin/java java [JAVA_PATH] 200
sudo update-alternatives --install /usr/bin/javac javac [JAVAC_PATH] 200
```

### 3 Compile

In the source directory, compile it:

```
cd [SCI_GIT_DIR]/scilab
export LD_LIBRARY_PATH=`pwd`/lib/thirdparty/
LD_LIBRARY_PATH=`pwd`/lib/thirdparty/ ./configure --prefix=[SCI_INSTALL_DIR]
make
make install
```

### 4 After Installation


If these files _libjava.so_, _libverify.so_, _libjvm.so_ are missing, try to find them in JRE directory or the thirdpart JRE directory:

```
ln -s /usr/workspace/git/scilab_git/scilab/java/jre1.8.0_51/lib/amd64/libjava.so libjava.so
ln -s /usr/workspace/git/scilab_git/scilab/java/jre1.8.0_51/lib/amd64/libverify.so libverify.so
ln -s /usr/workspace/git/scilab_git/scilab/java/jre1.8.0_51/lib/amd64/server/libjvm.so libjvm.so
```

You could aslo try to copy the thirdpart libraries to the scilab directory if you don't want to set the _LD_LIBRARY_PATH_ env variable.

```
cp -r [SCI_GIT_DIR]/scilab/thirdparty/ [SCI_INSTALL_DIR]/
cp -r [SCI_GIT_DIR]/scilab/lib/thirdparty/ [SCI_INSTALL_DIR]/lib/
```

And you might also need to modify the _librarypath.xml_ file in [SCI_INSTALL_DIR]/share/scilab/etc.

    <path value="$SCILAB/../../bin"/>
    <path value="$SCILAB/../../lib/scilab/"/>
    <path value="$SCILAB/../../lib/thirdparty/"/>

### 5 Run

In the scilab install directory [SCI_INSTALL_DIR]:

```
bin/scilab
```

### References

1. [Compilation of Scilab](https://wiki.scilab.org/Compilation%20of%20Scilab)
2. [Compiling Scilab 5.x under GNU-Linux Unix](https://wiki.scilab.org/Compiling%20Scilab%205.x%20under%20GNU-Linux%20Unix)
3. [Dependencies of Scilab 5.X](https://wiki.scilab.org/Dependencies%20of%20Scilab%205.X)



