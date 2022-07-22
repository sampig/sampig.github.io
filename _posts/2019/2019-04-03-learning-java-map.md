---
layout: post
title: "Learning Java: How to Use Maps"
date: 2019-04-03 22:00:00 +0100
category: tutorial
tagline: "HashMap vs. TreeMap(SortedMap) vs. LinkedHashMap vs. Hashtable"
tags: [Java]
abstract : "Learning Note: comparing HashMap, TreeMap(SortedMap), LinkedHashMap and Hashtable."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Inheritance Review](#inheritance-review)
* [Understanding Classes](#understanding-classes)
    - [HashMap](#hashmap)
    - [LinkedHashMap](#linkedhashmap)
    - [TreeMap](#treemap)
    - [Hashtable](#hashtable)
* [Comparison](#comparison)
* [Summary](#summary)
* [References](#references)


## Introduction

The structure of key-value pair map is important in programming.
Java provides a basic interface _Map_ and several classes such as _HashMap_, _TreeMap_ and _LinkedHashMap_ that implement the interface.
I will mainly compare these classes, _HashMap_, _LinkedHashMap_ and _TreeMap_.


## Inheritance Review

The _Map_ interface has many implementing classes. And some of these classes also have sub-classes.

```
Interface Map<K, V>
All Known Subinterfaces:
    Bindings, ConcurrentMap<K,V>, ConcurrentNavigableMap<K,V>, LogicalMessageContext, MessageContext, NavigableMap<K,V>, SOAPMessageContext, SortedMap<K,V>
All Known Implementing Classes:
    AbstractMap, Attributes, AuthProvider, ConcurrentHashMap, ConcurrentSkipListMap, EnumMap, HashMap, Hashtable, IdentityHashMap, LinkedHashMap, PrinterStateReasons, Properties, Provider, RenderingHints, SimpleBindings, TabularDataSupport, TreeMap, UIDefaults, WeakHashMap
```

```
Class HashMap<K,V>
extends AbstractMap<K,V>
implements Map<K,V>, Cloneable, Serializable
```

```
class TreeMap<K,V>
extends AbstractMap<K,V>
implements NavigableMap<K,V>, Cloneable, Serializable
```

```
class AbstractMap<K,V>
extends Object
implements Map<K,V>
```

```
interface SortedMap<K,V>
extends Map<K,V>
```

```
class Hashtable<K,V>
extends Dictionary<K,V>
implements Map<K,V>, Cloneable, Serializable
```

```
class LinkedHashMap<K,V>
extends HashMap<K,V>
implements Map<K,V>
```


## Understanding Classes

An object that maps keys to values. A map cannot contain duplicate keys; each key can map to at most one value.
The _Map_ interface provides three collection views, which allow a map's contents to be viewed as a set of keys, collection of values, or set of key-value mappings.

Basically, these classes that implement _Map_ are like:
- _HashMap_ is implemented based on a hash table.
- _LinkedHashMap_ is like a HashMap, but in insertion order or in least-recently-used (LRU) order.
- _TreeMap_ is implemented based on a red-black tree.
- _WeakHashMap_ is a map of weak keys that allow objects referred to by the map to be released.
- _ConcurrentHashMap_ is a thread-safe map which does not involve synchronization locking.
- _IdentityHashMap_ is a hash map that uses `==` instead of `equals()` to compare keys.

### HashMap

Hash table based implementation of the Map interface. The HashMap class is roughly equivalent to Hashtable.

HashMap offers O(1) lookup and insertion. If you iterate through the keys, though, the ordering of the keys is essentially arbitrary. It is implemented by an array of linked lists.
- A HashMap contains values based on the key.
- It contains only unique elements.
- It may have one null key and multiple null values.
- It makes no guarantees as to the order of the map; in particular, it does not guarantee that the order will remain constant over time.
- It provides constant-time performance for the basic operations (get and put), assuming the hash function disperses the elements properly among the buckets. Iteration over collection views requires time proportional to the "capacity" of the HashMap instance (the number of buckets) plus its size (the number of key-value mappings). Thus, it's very important not to set the initial capacity too high (or the load factor too low) if iteration performance is important.
- It is not synchronized. If multiple threads access a hash map concurrently, and at least one of the threads modifies the map structurally, it must be synchronized externally.

### LinkedHashMap

LinkedHashMap is a subclass of HashMap.

LinkedHashMap offers O(1) lookup and insertion. Keys are ordered by their insertion order. It is implemented by doubly-linked buckets.
- A LinkedHashMap contains values based on the key.
- It contains only unique elements.
- It may have one null key and multiple null values.
- It maintains insertion order or LRU order. If you want to use LRU order, you need to change one parameter.
- Different from HashMap in that it maintains a doubly-linked list running through all of its entries. This linked list defines the iteration ordering, which is normally the order in which keys were inserted into the map (insertion-order). Note that insertion order is not affected if a key is re-inserted into the map.
- Same with HashMap, it is not synchronized, either.

### TreeMap

TreeMap is implemented NavigableMap whose super interface are SortedMap and Map.

TreeMap offers O(log N) lookup and insertion. Keys are ordered, so if you need to iterate through the keys in sorted order, you can. This means that keys must implement the Comparable interface.
- A TreeMap contains values based on the key. It implements the NavigableMap interface and extends AbstractMap class.
- It contains only unique elements.
- It cannot have null key but can have multiple null values.
- It is sorted according to the natural ordering of its keys, or by a Comparator provided at map creation time, depending on which constructor is used.
- It is not synchronized.

### Hashtable

The basic _Hashtable_ is very similar to the _HashMap_.
- A Hashtable is an array of list. Each list is known as a bucket. The position of bucket is identified by calling the hashcode() method. A Hashtable contains values based on the key.
- It contains only unique elements.
- Any non-null object can be used as a key or as a value.

> According to Java API, _Hashtable_ is synchronized, unlike the new collection implementations.
> If a thread-safe implementation is not needed, it is recommended to use _HashMap_ in place of _Hashtable_.
> If a thread-safe highly-concurrent implementation is desired, then it is recommended to use _ConcurrentHashMap_ in place of _Hashtable_.


## Comparison

| Property | HashMap | LinkedHashMap | TreeMap |
|----------|---------|---------------|---------|
| Time complexity | O(1) | O(1) | O(log N) |
| Iteration order | random | in insertion order or LRU order | in sorted order by key |
| Null keys | allowed | allowed | not allowed |
| Synchronization | none | none | none |
| Data structure | list of buckets | doubly linked list of buckets | red-black implementation of binary tree |
| Requirements for keys | `equals()` and `hashCode()` | `equals()` and `hashCode()` | `Comparable` needs to be implemented |

A simple testing example for insertion:

```java
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.TreeMap;

public class SimpleTest {

    private int[] integers = { 1, -2, 0, 3, -4 };

    public void testHashMap() {
        HashMap<Integer, String> map = new HashMap<Integer, String>();
        for (int i : integers) {
            map.put(i, Integer.toString(i));
        }
        System.out.print("HashMap oder: ");
        System.out.println(map);
    }

    public void testLinkedHashMap() {
        LinkedHashMap<Integer, String> map = new LinkedHashMap<Integer, String>(0, 0.75f, true);
        for (int i : integers) {
            map.put(i, Integer.toString(i));
        }
        System.out.print("LinkedHashMap oder: ");
        System.out.println(map);
        map.get(integers[2]);
        System.out.print("LinkedHashMap oder after accessing: ");
        System.out.println(map);
    }

    public void testTreeMap() {
        TreeMap<Integer, String> map = new TreeMap<Integer, String>();
        for (int i : integers) {
            map.put(i, Integer.toString(i));
        }
        System.out.print("TreeMap oder: ");
        System.out.println(map);
    }

    public static void main(String... strings) {
        SimpleTest st = new SimpleTest();
        st.testHashMap();
        st.testHashMap();
        st.testLinkedHashMap();
        st.testTreeMap();
    }

}

/*
Output:
HashMap oder: {0=0, 1=1, -2=-2, 3=3, -4=-4}
HashMap oder: {0=0, 1=1, -2=-2, 3=3, -4=-4}
LinkedHashMap oder: {1=1, -2=-2, 0=0, 3=3, -4=-4}
LinkedHashMap oder after accessing: {1=1, -2=-2, 3=3, -4=-4, 0=0}
TreeMap oder: {-4=-4, -2=-2, 0=0, 1=1, 3=3}
*/
```


## Summary

In a conclusion, you could use HashMap if there are no special requirements, because it is faster and requires less overhead.
If insertion order is important, use LinkedHashMap.
If the order of key is important, use TreeMap.


## References

1. _Thinking in Java (4th Edition)_ by Bruce Eckel - Understanding Maps
2. [Java 8 API Specification - Map](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html){:target="_blank"}
3. [Differences between TreeMap, HashMap and LinkedHashMap in Java](https://www.geeksforgeeks.org/differences-treemap-hashmap-linkedhashmap-java/){:target="_blank"}
4. [HashMap vs. TreeMap vs. Hashtable vs. LinkedHashMap](https://www.programcreek.com/2013/03/hashmap-vs-treemap-vs-hashtable-vs-linkedhashmap/){:target="_blank"}
5. [Hashmap in Java - Scaler Topics](https://www.scaler.com/topics/java/hashmap-in-java/){:target="_blank"}
