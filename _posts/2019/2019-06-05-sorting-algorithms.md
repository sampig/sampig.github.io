---
layout: post
title: "Learning Algorithm: Sorting"
date: 2019-06-05 13:15:00 +0200
category: tutorial
tagline: ""
tags: [Algorithm]
abstract : "Learning Note: a comparison of sorting algorithms."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Comparison](#comparison)
    - [Insertion Sort](#insertion-sort)
    - [Shell Sort](#shell-sort)
    - [Heapsort](#heapsort)
    - [Mergesort](#mergesort)
    - [Quicksort](#quicksort)
    - [Bucket Sort](#bucket-sort)
    - [Bubble Sort](#bubble-sort)
    - [Selection Sort](#selection-sort)
* [Source Code](#source-code)
* [External Sorting](#external-sorting)
* [References](#references)


# Introduction

Sorting is algorithms that put elements of an array in a certain order.
Efficient sorting is important for what require sorted data.

In this blog, the assumption for these algorithms is that the entire sort can be done in main memory.


# Comparison

A basic comparison of some algorithms:

| Name | Best | Average | Worst | Memory | Stable | Comment |
|------|------|---------|-------|--------|--------|---------|
| Insertion sort | &Omega;(N) | &Theta;(N<sup>2</sup>) | O(N<sup>2</sup>) | 1 | Yes |  |
| Shell sort | &Omega;(N*log(N)) | Depends on gap sequence | Depends on gap sequence; best known is O(N<sup>4/3</sup>) | 1 | No |  |
| Heapsort | &Omega;(N*log(N)) (N if all keys are not distinct) | &Theta;(N*log(N)) | O(N*log(N)) | 1 | No |  |
| Mergesort | &Omega;(N*log(N)) | &Theta;(N*log(N)) | O(N*log(N)) | n | Yes |  |
| Quicksort | &Omega;(N*log(N)) | &Theta;(N*log(N)) | O(N<sup>2</sup>) | log(N) | Both |  |
| Bucket Sort | &Omega;(N+M) | &Theta;(N+M) | O(N<sup>2</sup>) | N+M | Yes | Use other sorting algorithms to sort buckets |
| Bubble Sort | &Omega;(N) | &Theta;(N<sup>2</sup>) | O(N<sup>2</sup>) | 1 | Yes |  |
| Selection Sort | &Omega;(N<sup>2</sup>) | &Theta;(N<sup>2</sup>) | O(N<sup>2</sup>) | 1 | No |  |

## Insertion Sort

Insertion sort is one of the simplest sorting algorithm that is quite suitable for small data but is less efficient on large data.

The steps of insertion sort are simple:
1. Loop the element from the second to the last.
2. Compare the element to the elements before it, and switch the places until it is larger.

![insertion sort](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)
<small>(Source: Wikipedia and Wikimedia)</small>

## Shell Sort

Shell sort is a generalization of insertion sort that allows the exchange of elements that are far apart.

The steps of shell sort are:
1. Sort pairs of elements far apart from each other by gap.
2. Reduce the gap and repeat until gap is 1.

![shell sort](https://upload.wikimedia.org/wikipedia/commons/d/d8/Sorting_shellsort_anim.gif)
<small>(Source: Wikipedia and Wikimedia)</small>

The worst case of shell sort is complicated and depends on the gap sequence.

## Heapsort

Heap sort is a comparison-based sorting algorithm using binary heap data structure.

The steps of heap sort are:
1. Build a max heap from the array. Then the largest element is at the root of the heap.
2. Swap the first element with the last element.
3. Build a max heap without considering the last element.
4. Then repeat the step 2 and step 3 until the considered range of elements is only one.

![heap sort](https://upload.wikimedia.org/wikipedia/commons/4/4d/Heapsort-example.gif)
<small>(Source: Wikipedia and Wikimedia)</small>

## Mergesort

Merge sort is an efficient comparison-based sorting algorithm.
The fundamental operation of merge sort is merging two sorted separated arrays.

The steps of merge sort are:
1. Divide the array into two arrays from the middle.
2. Repeat the division until each array contains only one element.
3. Repeat merging pairs of arrays by comparison of elements.

![merge sort](https://upload.wikimedia.org/wikipedia/commons/e/e6/Merge_sort_algorithm_diagram.svg)
<small>(Source: Wikipedia and Wikimedia)</small>

## Quicksort

Quick sort is a divide and conquer algorithm. It is quite efficient.

The steps of quick sort are:
1. Pick an element called a pivot. Normally, you can pick the first one, the last one, the median one or a random one. But it is a risk to choose the first or the last when the array is pre-ordered.
2. Partitioning: reorder the array so that all elements that are less than the pivot come before the pivot and all elements that are larger than the pivot come after the pivot.
3. Recursively apply the above steps to the sub-array.

![quick sort](https://upload.wikimedia.org/wikipedia/commons/a/af/Quicksort-diagram.svg)
<small>(Source: Wikipedia and Wikimedia)</small>

## Bucket Sort

Bucket sort is a distribution sort that works by putting elements into some buckets.

The steps of bucket sort are:
1. Create several empty buckets.
2. According to the distribution and range of each buckets, put each element into its corresponded bucket.
3. Sort each non-empty bucket using one of the simple sort algorithms.
4. Concatenate the buckets in order or put all elements into the original array based on the order of buckets.

![bucket sort1](https://upload.wikimedia.org/wikipedia/commons/6/61/Bucket_sort_1.svg)
![bucket sort2](https://upload.wikimedia.org/wikipedia/commons/e/e3/Bucket_sort_2.svg)
<small>(Image source: Wikipedia and Wikimedia)</small>

## Bubble Sort

Bubble sort is a simple sorting algorithm that repeatedly compares adjacent pairs and swaps them if they are in wrong order.

![bubble sort](https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif)
<small>(Source: Wikipedia and Wikimedia)</small>

## Selection Sort

The basic idea of selection sort is finding the minimum element repeatedly.

The steps of selection sort are:
1. Find the minimum element from the array.
2. Move it to the front of the array.
3. Find the minimum element from the rest part of the array.
4. Move it to the front of the sub-array.
5. Repeat step 3 and step 4.

![selection sort](https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif)
<small>(Source: Wikipedia and Wikimedia)</small>


# Source Code

The sources of implementation for these sorting algorithms can be found in my [GitHub](https://github.com/sampig/ZhuzhuLearning/tree/master/Algorithm){:target="_blank"}.


# External Sorting

Sorting that cannot be performed in main memory and must be done on disk is also important.

There are some external sorting algorithms such as external merge sort(multiway merge, polyphase merge, replacement selection) and external distribution sort.


# References

1. "_Data Structures and Algorithm Analysis in Java_" by Mark A. Weiss.
2. 《数据结构（C语言）》 by 严蔚敏 吴伟民
3. [GitHub - ZhuzhuLearning/Algorithm](https://github.com/sampig/ZhuzhuLearning/tree/master/Algorithm){:target="_blank"}
