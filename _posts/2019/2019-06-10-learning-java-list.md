---
layout: post
title: "Learning Java: How to Use java.util.List"
date: 2019-06-10 12:15:00 +0200
category: tutorial
tagline: "ArrayList vs. LinkedList"
tags: [Java]
abstract : "Learning Note: learn how to use List and compare ArrayList and LinkedList in Java."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Inheritance Review](#inheritance-review)
* [Understanding Classes](#understanding-classes)
    - [ArrayList](#arraylist)
    - [LinkedList](#linkedlist)
* [Comparison](#comparison)
    - [Add Operation](#add-operation)
    - [Get Operation](#get-operation)
    - [Remove Operation](#remove-operation)
    - [Iteration](#iteration)
    - [Memory](#memory)
    - [An Example](#an-example)
* [Summary](#summary)
* [References](#references)


# Introduction

_List_ is one type of _Collection_. The other two types of _Collection_ are _Set_ and _Queue_.
A _List_ holds the elements in the way that they were inserted.

_List_ promises to maintain elements in a particular sequence.
The _List_ interface adds a number of methods to _Collection_ that allow insertion and removal of elements in the middle of a _List_.

> There are two _List_ in Java default package. One is a collection interface in _java.util_ package and the other is a GUI component class in _java.awt_ package.

There are two types of _List_: _ArrayList_ and _LinkedList_.
I will compare them in this blog.


# Inheritance Review

The _java.util.List_ interface has several implementing classes.

```
Interface List<E>
All Superinterfaces:
    Collection<E>, Iterable<E>
All Known Implementing Classes:
    AbstractList, AbstractSequentialList, ArrayList, AttributeList, CopyOnWriteArrayList, LinkedList, RoleList, RoleUnresolvedList, Stack, Vector
```

```
public class ArrayList<E>
extends AbstractList<E>
implements List<E>, RandomAccess, Cloneable, Serializable
```

```
public class LinkedList<E>
extends AbstractSequentialList<E>
implements List<E>, Deque<E>, Cloneable, Serializable
```


# Understanding Classes

A _List_ is simple to use: call `add()` to insert objects, call `get()` to get one of them out at a time, and call `iterator()` to get an _Iterator_ for the sequence.

There are also some other useful methods such as `remove()`, `indexOf()`, `contains()`, `containsAll()`, `subList()`, `retainAll()`, `removeAll()`, `set()`, `addAll()`, `isEmpty()` and `clear()`.
`Collections.addAll()` runs much faster than `.addAll()`.

The _List_ interface provides a special iterator, called a _ListIterator_, that allows element insertion and replacement, and bidirectional access in addition to the normal operations that the Iterator interface provides. A method is provided to obtain a list iterator that starts at a specified position in the list.

It is possible to use the output of `Arrays.asList()` directly as a new _List_. But the underlyting representation in this case is the array which cannot be resized.

```java
Random rand = new Random();

List<Player> players = PlayerCreator.generateArrayList(5);
System.out.println("01 players: " + players);

Defender d = new Defender("Barzagli");
players.add(d);
System.out.println("02 players: " + players);
System.out.println("03 players.contains: " + players.contains(d));
players.remove(d);
System.out.println("04 players: " + players);

Player p2 = players.get(2);
System.out.println("05 p2:" + p2 + " in " + players.indexOf(p2));

Player g = new Goalkeeper();
System.out.println("06 players.indexOf: " + players.indexOf(g));
System.out.println("07 players.remove: " + players.remove(g));

System.out.println("08 players: " + players);
players.add(3, new Forward());
System.out.println("09 players: " + players);

List<Player> sub = players.subList(1, 3);
System.out.println("10 subList: " + sub);
System.out.println("11 containsAll: " + players.containsAll(sub));
Collections.sort(sub);
System.out.println("12 sorted sub: " + sub);
System.out.println("13 containsAll: " + players.containsAll(sub));
Collections.shuffle(sub, rand);
System.out.println("14 shuffle: " + sub);
System.out.println("15 containsAll: " + players.containsAll(sub));

List<Player> copy = new ArrayList<Player>(players);
System.out.println("16 copy: " + copy);
sub = Arrays.asList(players.get(1), players.get(3));
System.out.println("17 sub: " + sub);
copy.retainAll(sub);
System.out.println("18 copy: " + copy);
copy = new ArrayList<Player>(players);
System.out.println("19 copy: " + copy);
copy.remove(2);
System.out.println("20 copy: " + copy);
copy.set(1, new Defender("Chiellini"));
System.out.println("21 copy: " + copy);
copy.addAll(2, sub);
System.out.println("22 copy: " + copy);

System.out.println("23 players: " + players);
System.out.println("24 players.isEmpty: " + players.isEmpty());
players.clear();
System.out.println("25 players: " + players);
System.out.println("26 players.isEmpty: " + players.isEmpty());
```

## ArrayList

`ArrayList` is the most basic type of sequence.
It excels at randomly accessing elements, but is slower when inserting and removing elements in the middle of a _List_.

## LinkedList

`LinkedList` implements it with a doubly-linked list.
It provides optimal sequential access with inexpensive insertion and deletions from the middle of the _List_.
It is relatively slow for random access, but has a larger feature set than the _ArrayList_.

_LinkedList_ provides some identical methods, such as `getFirst()`, `element()`, `removeFirst()`, `offer()` and `removeLast()`.


# Comparison

Both `ArrayList` and `LinkedList` are implementation of `List` interface. They have something in common:
1. Both of them hold elements in the same order in which they are inserted.
2. Both of them are non-synchronized and can be made synchronized explicitly by using Collections.synchronizedList method.

The difference between the two is not only performance for certain types of operations, but also that a _LinkedList_ contains more operations than a _ArrayList_.

| Methods | ArrayList | LinkedList |
|---------|-----------|------------|
| add(E element) | O(1) | O(1) |
| add(int, E)    | O(N) (N/2 on average) | O(N) (N/4 on average) |
| get(int index) | __O(1)__ | O(N) |
| set(int, E)    | __O(1)__ | O(N) |
| remove(int)    | O(N) (N/2 on average) | O(N) (N/4 on average) |
| ListIterator.add(E) | O(N) | __O(1)__ |
| Iterator.remove()   | O(N) | __O(1)__ |

## Add Operation

For normally appending operation `add(E)`, both performs almost the same, __O(1)__.
However, `ArrayList` needs to resize its array if it is out of its capacity. In this case, it will take more time and the worst-case might be __O(N)__.

For the insertion operation `add(int, E)`, `LinkedList` performs better than `ArrayList`.
If the insertion index is random, `ArrayList` might perform better because the cost of random access in `LinkedList` is quite high.
If the size of list is larger and the insertion index is less (in this case, the cost of the random access could be negligible), `LinkedList` will perform significantly better.

## Get Operation

For the access operation `get(int)`, the accesses for `ArrayList` are faster and very consistent regardless of the list size, __O(1)__.
Because it will directly find the element at given index location.
For `LinkedList`, the access times grow very significantly for larger lists.
Because it need to traverse the elements from the first one to the correct one. The worst case might be __O(N)__.

The `set(int, E)` method is similar to `get(int)` method because the main cost is the access action.

## Remove Operation

For the removal operation `remove(int)`, `LinkedList` performs a little better than `ArrayList` on average.
But if the list size is large and the removal index is less(in this case, the cost of the random access could be negligible), `LinkedList` will be much better.

`ArrayList` needs to move all elements on right. Then the worst case could be __O(N)__.
`LinkedList` just needs to reset the pointers of previous and next elements. No copy or movement is required. The performance is __O(1)__ ignoring the cost of accessing.

## Iteration

An iterator is an object whose job is to move through a sequence and select each object in that sequence.
Iteration is the __O(N)__ operation for both `ArrayList` and `LinkedList`.

But ignoring the iteration cost, the performances for iteration insertion `ListIterator.add(E)` and iteration removal `Iterator.remove()` are different.
For `ArrayList`, these operations get expensive as the list gets larger, but for `LinkedList`, it is relatively cheap and constant regardless of size.
Because `ArrayList` must create space and copy all its references forward during an insertion. The worst case could be __O(N)__.
`LinkedList` only needs to link in a new element and does not have to modify the rest of the list. The performance is __O(1)__.

## Memory

`ArrayList` only maintains indexes and element data.
But `LinkedList` contains element data and two pointers for the previous and next elements.
So the memory consumption is higher in `LinkedList`.

## An Example

This example is the source in the book _Thinking in Java (4th Edition)_ by Bruce Eckel.
The codes below are some parts of the whole program.
I also modified and added some other tests.

```java
public class ListPerformance {

    static Random rand = new Random();
    static int reps = 1000;
    static List<Test<List<Integer>>> tests = new ArrayList<Test<List<Integer>>>();
    static List<Test<LinkedList<Integer>>> qTests = new ArrayList<Test<LinkedList<Integer>>>();
    static {
        tests.add(new Test<List<Integer>>("add") {
            int test(List<Integer> list, TestParam tp) {
                int loops = tp.loops;
                int listSize = tp.size;
                for (int i = 0; i < loops; i++) {
                    list.clear();
                    for (int j = 0; j < listSize; j++) {
                        list.add(j);
                    }
                }
                return loops * listSize;
            }
        });
        tests.add(new Test<List<Integer>>("get") {
            int test(List<Integer> list, TestParam tp) {
                int loops = tp.loops * reps;
                int listSize = list.size();
                for (int i = 0; i < loops; i++) {
                    list.get(rand.nextInt(listSize));
                }
                return loops;
            }
        });
        tests.add(new Test<List<Integer>>("set") {
            int test(List<Integer> list, TestParam tp) {
                int loops = tp.loops * reps;
                int listSize = list.size();
                for (int i = 0; i < loops; i++) {
                    list.set(rand.nextInt(listSize), 47);
                }
                return loops;
            }
        });
        tests.add(new Test<List<Integer>>("iteradd") {
            int test(List<Integer> list, TestParam tp) {
                final int LOOPS = 1000000;
                int half = list.size() / 2;
                ListIterator<Integer> it = list.listIterator(half);
                for (int i = 0; i < LOOPS; i++) {
                    it.add(47);
                }
                return LOOPS;
            }
        });
        tests.add(new Test<List<Integer>>("insert") {
            int test(List<Integer> list, TestParam tp) {
                int loops = tp.loops;
                for (int i = 0; i < loops; i++) {
                    list.add(rand.nextInt(list.size()), 47);
                }
                return loops;
            }
        });
        tests.add(new Test<List<Integer>>("insert5") {
            int test(List<Integer> list, TestParam tp) {
                int loops = tp.loops;
                for (int i = 0; i < loops; i++) {
                    list.add(5, 47);
                }
                return loops;
            }
        });
        tests.add(new Test<List<Integer>>("insertl") {
            int test(List<Integer> list, TestParam tp) {
                int loops = tp.loops;
                for (int i = 0; i < loops; i++) {
                    list.add(tp.size - 5, 47);
                }
                return loops;
            }
        });
        tests.add(new Test<List<Integer>>("remove") {
            int test(List<Integer> list, TestParam tp) {
                int loops = tp.loops;
                int size = tp.size;
                for (int i = 0; i < loops; i++) {
                    list.clear();
                    list.addAll(new CountingIntegerList(size));
                    while (list.size() > 5) {
                        list.remove(5);
                    }
                }
                return loops * size;
            }
        });
        tests.add(new Test<List<Integer>>("iterrm") {
            int test(List<Integer> list, TestParam tp) {
                int loops = tp.loops;
                int size = tp.size;
                for (int i = 0; i < loops; i++) {
                    list.clear();
                    list.addAll(new CountingIntegerList(size));
                    Iterator<Integer> it = list.iterator();
                    while (it.hasNext()) {
                        it.next();
                        it.remove();
                    }
                }
                return loops * size;
            }
        });
    }

    static class ListTester extends Tester<List<Integer>> {

        public ListTester(List<Integer> container, List<Test<List<Integer>>> tests) {
            super(container, tests);
        }

        @Override
        protected List<Integer> initialize(int size) {
            container.clear();
            container.addAll(new CountingIntegerList(size));
            return container;
        }

        public static void run(List<Integer> list, List<Test<List<Integer>>> tests) {
            new ListTester(list, tests).timedTest();
        }

    }

    public static void main(String... strings) {
        Tester<List<Integer>> arrayTest = new Tester<List<Integer>>(null, tests.subList(1, 3)) {
            @Override
            protected List<Integer> initialize(int size) {
                Integer[] ia = new Integer[size];
                return Arrays.asList(new CountingIntegerList(size).toArray(ia));
            }
        };
        arrayTest.setHeadline("Array as List");
        arrayTest.timedTest();
        Tester.defaultParams = TestParam.array(10, 5000, 100, 5000, 1000, 1000, 10000, 200);
        ListTester.run(new ArrayList<Integer>(), tests);
        ListTester.run(new LinkedList<Integer>(), tests);
        Tester.fieldWidth = 12;
    }

}
```

The output:

```
--- Array as List ---
 size     get     set
   10      23      25
  100      22      24
 1000      23      25
10000      19      27
--------------------------------- ArrayList ---------------------------------
 size     add     get     set iteradd  insert insert5 insertl  remove  iterrm
   10     138      28      30      61     749     826     869     348     548
  100      57      26      25      57     865    1171    1166     125     175
 1000      43      37      24     157     574     591     324     242     326
10000      25      32      41    1335    1714    4429     168    1413    1272
--------------------------------- LinkedList ---------------------------------
 size     add     get     set iteradd  insert insert5 insertl  remove  iterrm
   10     167      55      53     120    3385     140     135     231     280
  100      30      80      82      93    2951      96     277      42      56
 1000      46     544     566     108    1150     100    1181      37      27
10000      25    7568    7488      31    7825     105     309      52      33
```

The performance of different functions between ArrayList and LinkedList is clear.

Some source codes can be found in my [GitHub](https://github.com/sampig/ZhuzhuLearning/tree/master/Java/src/org/zhuzhu/learning/containers){:target="_blank"}.


# Summary

In one word, `ArrayList` is better for accessing elements and `LinkedList` is better for manipulating elements.

Normally, most people would use `ArrayList` if there are no special requirements because both of them are similar for small datasets.
If many search (`get(int)`) operations are needed or many random accesses are required to be performed, it is better to use `ArrayList`.
If many insertion or removal operations are frequent, `LinkedList` would be a good choice.


# References

1. _Thinking in Java (4th Edition)_ by Bruce Eckel
2. [Java 8 API Specification - List](https://docs.oracle.com/javase/8/docs/api/java/util/List.html){:target="_blank"}
3. [Difference between LinkedList vs ArrayList in Java](https://howtodoinjava.com/java/collections/arraylist/linkedlist-vs-arraylist/){:target="_blank"}
4. [When to use LinkedList over ArrayList in Java?](https://stackoverflow.com/questions/322715/when-to-use-linkedlist-over-arraylist-in-java){:target="_blank"}
5. [GitHub - ZhuzhuLearning](https://github.com/sampig/ZhuzhuLearning/tree/master/Java/src/org/zhuzhu/learning/containers){:target="_blank"}
