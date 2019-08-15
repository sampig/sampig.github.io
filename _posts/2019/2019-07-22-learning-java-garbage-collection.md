---
layout: post
title: "Learning Java: Garbage Collection in Java"
date: 2019-07-22 23:15:00 +0200
category: tutorial
tagline: ""
tags: [Java]
abstract : "Learning Note: how does garbage collection work in Java."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [How a Garbage Collector Works](#how-a-garbage-collector-works)
    - [How to Identify Garbage](#how-to-identify-garbage)
        + [Reference Counting](#reference-counting)
        + [Reachability Analysis](#reachability-analysis)
    - [How to Collect Garbage](#how-to-collect-garbage)
        + [Stop and Copy](#stop-and-copy)
        + [Mark and Sweep](#mark-and-sweep)
        + [Mark and Compact](#mark-and-compact)
* [Garbage Collection in Java](#garbage-collection-in-java)
    - [Finalization and Termination Condition](#finalization-and-termination-condition)
    - [Java Memory Management and Garbage Collection](#java-memory-management-and-garbage-collection)
* [Summary](#summary)
* [References](#references)


# Introduction

Garbage Collection (GC) is a form of automatic memory management. Its aim is to reclaim garbage or memory occupied by objects that are no longer in use by the program.
Garbage collection was invented by John McCarthy around 1959 to simplify manual memory management in [Lisp](http://www-formal.stanford.edu/jmc/history/lisp/lisp.html){:target="_blank"}.
It has a longer history than Java.


# How a Garbage Collector Works

There are several garbage-collection schemes.

## How to Identify Garbage

First of all, we need to find out what should be considered as garbages and which storages should be released.

### Reference Counting

Reference Counting(引用计数算法) is a simple but slow scheme.

In this scheme, each object contains a reference counter.
Every time a reference is attached to that object, its reference counter is increased.
Every time a reference goes out or is set to null, its counter is decreased.
Once the reference counter of an object becomes zero, that storage will be released.

But one shortcoming is that if objects circularly refer to each other they can have nonzero reference counts.
Below is an example:
```java
public class ReferenceCountingGC {
    public Object instance;
    public static void main(String...strings) {
        ReferenceCountingGC a = new ReferenceCountingGC(); // 1st instance
        ReferenceCountingGC b = new ReferenceCountingGC(); // 2nd instance
        a.instance = b;
        b.instance = a;
        a = null;
        b = null;
    }
}
```

It creates two instances.
The first instance has two references, one is from a and the other is from b.instance. The second instance also has two references.
After two variables are set to null, the two instances still have one reference from their members.
In this case, their reference counter will never be zero.

Another drawback is that reference counting scheme requires extra space for each object to store its reference counter and extra process resource to deal with counter.

### Reachability Analysis

The basic idea of Reachability Analysis(可达性分析算法) is to trace which objects are reachable by a chain of references from "root" objects.
The "root" is called GC Roots and the path from root to the certain object is called reference chain.
If one object cannot be reachable from any GC Roots, it will be considered as garbage and the storage will be released.

As shown in the image below, the objects in blue rectangle should be kept alive and the objects in gray rectable can be recycled:
![GC Roots]({{ site.url }}/assets/images/java_gc/gc_roots.png){:height="300px" width="600px"}

In Java, there are 4 types of objects can be used as GC Roots:
1. objects referenced in VM Stack;
2. objects referenced by static members or methods in Method Area;
3. objects referenced by constants in Method Area;
4. objects referenced by JNI in Native Method Stack.

```java
public class ReachabilityAnalysisGC {
    public static ReachabilityAnalysisGC staticMember;
    public static final ReachabilityAnalysisGC finalMember = new ReachabilityAnalysisGC("FinalMember");
    public ReachabilityAnalysisGC(String name) {}
    public static void main(String...strings) {
        ReachabilityAnalysisGC ragc = new ReachabilityAnalysisGC("first");
        ragc.staticMember = new ReachabilityAnalysisGC("StaticMember");
        ragc = null;
    }
}
```

In the example above, instance `ragc` can be used as GC Root.
When it is set to null. The string "first" can be recycled.
But the static member `staticMember` and the final member `finalMember` will not be recycled.

## How to Collect Garbage

After garbage identification, the collector will collect the garbages and release the storage.
But another important factor is the efficiency.

### Stop and Copy

Stop-and-Copy algorithm divides memory into two equal sections(heaps).
Every time only one section will be used.
When the program stops and the collection stars, all live objects are copied from one heap to another, leaving behind all the garbages.
In addition, as the objects are copied into the new heap, they are packed end-to-end and compacting the new heap.

There are two issues for this algorithm.
The first one is that two heaps are needed. So that we have to maintain twice as much memory as we actually need and it is kind of waste.
The second one is the copying process itself. The program needs to spend some time and resources on running the copying process no matter how many garbages there are. Besides, all references that point at the object must be hcanged.

### Mark and Sweep

Mark-and-Sweep algorithm has 2 steps.
In the first step - mark, it traces through all the references to find live objects or dead objects, and marks them.
During the second step - sweep, the dead objects will be released and the storage can be used again.

One big problem of this algorithm is memory fragments.
Since the dead objects might be stored in different parts of memory, the memory will be split into several parts when they are released.
It will cause that the memory cannot be used even there are a lot of spaces.

### Mark and Compact

Mark-and-Compact algorithm is similar to Mark-and-Sweep algorithm.
After marking the live objects and the dead objects, it will move all the live objects to the end.
Then all the storage that can be collected and is not used will be in the other end together.

It solves the problem of memory fragments and memory waste.
But it is much slower than other two algorithms.


# Garbage Collection in Java

## Finalization and Termination Condition

Java has its own garbage collector that only knows how to release memory allocated with __new__.
And it also provides a method called __finalize()__ to release the object's special memory.

The basic process of this is like:
"When the garbage collector is ready to release the storage used for object, it will first call finalize(), and only on the next garbage-collection pass will it reclaim the object's memory."

Something must be remembered:
1. "_Your objects might not get garbage collected._"
2. "_Garbage collection is not destruction._"
3. "_Garbage collection is only about memory._"

Unlike in C++ (if object was created using new in C++, the destructor is called when calling delete operator), Java doesn't provide a similar method for releasing objects.

In Java, __System.gc()__ is used to force finalization.
However, neither garbage collection nor finalization is guaranteed.

In some classes, their instances should be in a state whereby their memory can be safely released when they are ready to be cleaned up.

## Java Memory Management and Garbage Collection

In fact, Java uses an algorithm called "Adaptive generational stop-and-copy mark-and-sweep collection".

The Heap in Java is split into several parts(generations): Young Generation, Old Generation(or Tenured Generation) and Permanent Generation. It is shown as below:

![Hotspot Heap Structure]({{ site.url }}/assets/images/java_gc/hotspot_heap_structure.png){:width="600px"}
<small>(Source: https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide5.png)</small>

The __Young Generation__ is where all new objects are allocated and aged. When the young generation fills up, this causes a minor garbage collection. Some surviving objects are aged and eventually move to the old generation.
The Young Generation is divided into __Eden__ and __Survivor Space__ that contains two equal sections.
Survivor Space is like a buffer space between Eden and Old Generation.

The __Old Generation__ is used to store long surviving objects.

The __Permanent Generation__ contains metadata required by the JVM to describe the classes and methods used in the application.

Normally:
1. Heap Space = Young Generation (1/3) + (Old Generation + Permanent Generation) (2/3)
2. Young Generation = Eden (8/10) + S0 (1/10) + S1 (1/10)

These Generations perform like stop-and-copy and mark-and-sweep.

There are a number of additional speedups possible in JVM. An especially important one involves the operation of the loader and what is called a just-in-time (JIT) compiler. A JIT compiler partially or fully converts a program into native machine code so that it doesn't need to be interpreted by JVM and thus runs much faster.


# Summary

In this blog, only some basic ideas about garbage collection are introduced.
More details and explanation can be found in the references.


# References

1. "_Thinking in Java (4th Edition)_" by Bruce Eckel - Cleanup: finalization and garbage collection.
2. "_深入理解Java虚拟机：JVM高级特性与最佳实践_" by 周志明 - 第3章　垃圾收集器与内存分配策略
3. [Managing Memory and Garbage Collection](https://docs.oracle.com/cd/E19159-01/819-3681/6n5srlhqf/index.html){:target="_blank"}
4. [Java Garbage Collection Basics](https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html){:target="_blank"}
