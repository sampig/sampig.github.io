---
layout: post
title: "Interview Questions: some interesting questions from Alibaba"
date: 2019-08-28 10:15:00 +0200
category: tutorial
tagline: ""
tags: [Algorithm, Data Structure]
abstract : "Some interesting interview questions from Alibaba."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Question List](#question-list)
    - [Question 1: Unidirectional Linked List](#question-1-unidirectional-linked-list)
    - [Question 2: Calculate Square Root of 2](#question-2-calculate-square-root-of-2)
    - [Question 3: Find kth Smallest in BST](#question-3-find-kth-smallest-in-bst)
    - [Question 4: LRU Cache Scheme](#question-4-lru-cache-scheme)
    - [Question 13: Calculate the Sum of Two Float Number](#question-13-calculate-the-sum-of-two-float-number)
    - [Question 21: Most Frequent Stack](#question-21-most-frequent-stack)
    - [Question 22: Remove kth-to-last Element in Linked List](#question-22-remove-kth-to-last-element-in-linked-list)
    - [Question 26: Quality Guarantee for a New Product](#question-26-quality-guarantee-for-a-new-product)
    - [Question 28: Synchronous Queue](#question-28-synchronous-queue)
* [References](#references)


# Introduction

Here only some questions are listed.
If you are interested, look at or download the original document in Chinese from [Aliyun](https://yq.aliyun.com/articles/699746?utm_content=g_1000054983&scene=126&from=singlemessage){:target="_blank"}.


# Question List

## Question 1: Unidirectional Linked List

Print a unidirectional linked list in reversed order.

Use recursion.

An official example of solutions:

```cpp
typedef struct node
{
    int data;
    struct node *next;
    node(int d):data(d),next(NULL){}
}node;

void reverse(node *head)
{
    if(NULL==head||NULL==head->next)
    {
        return;
    }
    node *prev=NULL;
    node *pcur=head->next;
    node *next;
    while(pcur!=NULL)
    {
        if(pcur->next==NULL)
        {
            pcur->next=prev;
            break;
        }
        next=pcur->next;
        pcur->next=prev;
        prev=pcur;
        pcur=next;
    }
    head->next=pcur;
    node *tmp=head->next;
    while(tmp!=NULL)
    {
        cout<<tmp->data<<"\t";
        tmp=tmp->next;
    }
}
```

Another example by me:
```java
public class UnidirectionLinkedListReverse {

    public void printList(UnidirectionNode node) {
        if (node.next != null) {
            System.out.print(node.data + " --> ");
            printList(node.next);
        } else {
            System.out.println(node.data);
        }
    }

    public void printListReverse(UnidirectionNode node) {
        if (node.next != null) {
            printListReverse(node.next);
            System.out.print(node.data + " <-- ");
        } else {
            System.out.print(node.data + " <-- ");
        }
    }

    public static void main(String[] args) {
        UnidirectionNode[] nodes = new UnidirectionNode[10];
        nodes[0] = new UnidirectionNode();
        for (int i = 1; i < 10; i++) {
            nodes[i] = new UnidirectionNode();
            nodes[i].data = i;
            nodes[i - 1].next = nodes[i];
        }
        UnidirectionLinkedListReverse printer = new UnidirectionLinkedListReverse();
        printer.printList(nodes[0]);
        printer.printListReverse(nodes[0]);
    }

}

class UnidirectionNode {

    int data;
    UnidirectionNode next;

    public UnidirectionNode() {
    }

    public UnidirectionNode(int data, UnidirectionNode next) {
        super();
        this.data = data;
        this.next = next;
    }

}
```

## Question 2: Calculate Square Root of 2

Calculate the square root value of 2 (rounded to 10
decimal places) without using math libraries.

Tips: binary search algorithm(二分搜索算法), Newton's method(牛顿迭代法).

```java
public class Sqrt2 {

    private static double EPSINON = 0.0000000001;

    public static double sqrt2() {
        double low = 1, high = 2;
        double mid = (low + high) / 2;
        while (high - low > EPSINON) {
            if (mid * mid < 2) {
                low = mid;
            } else {
                high = mid;
            }
            mid = (high + low) / 2;
        }
        return mid;
    }

    public static void main(String[] args) {
        System.out.println(sqrt2());
    }

}
```

## Question 3: Find kth Smallest in BST

Find the kth smallest node in a binary search tree.

Tips: recursion.

```java
public class BinarySearchTree {

    static TreeNode generateTree() {
        TreeNode root = new TreeNode(5);
        TreeNode left = new TreeNode(3);
        TreeNode right = new TreeNode(6);
        root.left = left;
        root.right = right;
        TreeNode ll = new TreeNode(2);
        left.left = ll;
        ll.left = new TreeNode(1);
        left.right = new TreeNode(4);
        return root;
    }

    static int kthSmallest(TreeNode root, int k) {
        return kthSmallestHelper(root, k).value;
    }

    private static ResultType kthSmallestHelper(TreeNode root, int k) {
        if (root == null) {
            return new ResultType(false, 0);
        }
        ResultType left = kthSmallestHelper(root.left, k);
        if (left.found) {
            return new ResultType(true, left.value);
        }
        if (k - left.value == 1) {
            return new ResultType(true, root.value);
        }
        ResultType right = kthSmallestHelper(root.right, k - left.value - 1);
        if (right.found) {
            return new ResultType(true, right.value);
        }
        return new ResultType(false, left.value + 1 + right.value);
    }

    public static void main(String[] args) {
        TreeNode root = generateTree();
        for (int k = 1; k <= 7; k++) {
            System.out.println(k + ": " + kthSmallest(root, k));
        }
    }

}

class TreeNode {
    int value;
    TreeNode left;
    TreeNode right;

    TreeNode(int value) {
        this.value = value;
    }
}

class ResultType {
    boolean found;
    int value;

    ResultType(boolean found, int value) {
        this.found = found;
        this.value = value;
    }
}
```

- The time complexity is O(N).
- The space complexity is O(1) (O(logN) if considering the resource for recursion.)

## Question 4: LRU Cache Scheme

Implement LRU(Least Recently Used) data structure.

Requirements:
1. methods include `get` and `put`.
2. `get(key)` return the value if key exists. Otherwise return -1.
3. `put(key, value)` insert the value if key doesn't exist. If the cache is full, remove the LRU element before inserting.

Tips: queue and key-value map.

```java
public class LruCacheScheme {

    public static void main(String[] args) {
        Object[][][] test = { { { "put" }, { "put" }, { "get" }, { "put" }, { "get" }, { "put" }, { "get" }, { "get" }, { "get" } },
                { { 1, 1 }, { 2, 2 }, { 1 }, { 3, 3 }, { 2 }, { 4, 4 }, { 1 }, { 3 }, { 4 } } };
        LruCache cache = new LruCache(2);
        for (int i = 0; i < test[0].length; i++) {
            String oper = (String) test[0][i][0];
            String key = ((Integer) test[1][i][0]).toString();
            if ("get".equals(oper)) {
                System.out.println(cache.get(key));
            } else {
                cache.put(key, test[1][i][1]);
            }
        }
    }

}

class LruCache {
    int capacity;
    List<String> keys;
    Map<String, Object> map;

    LruCache(int capacity) {
        this.capacity = capacity;
        keys = new ArrayList<>(0);
        map = new HashMap<>(0);
    }

    void visitKey(String key) {
        if (keys.contains(key)) {
            keys.remove(key);
        }
        keys.add(key);
    }

    void elimKey() {
        String key = keys.get(0);
        keys = keys.subList(1, keys.size());
        map.remove(key);
    }

    Object get(String key) {
        if (!keys.contains(key)) {
            return -1;
        }
        visitKey(key);
        return map.get(key);
    }

    void put(String key, Object value) {
        if (!keys.contains(key)) {
            if (keys.size() == capacity) {
                elimKey();
            }
        }
        map.put(key, value);
        visitKey(key);
    }
}
```

The output is `1 -1 -1 3 4`.

## Question 13: Calculate the Sum of Two Float Number

Tips:
1. Directly plus on floating number on computer will cause lack of precision.
2. Plus the integer parts and plus the decimal parts.
3. Multiplying or dividing the decimal part by 100 will also cause lack of precision.
4. Convert the decimal parts into integer using strings.

## Question 21: Most Frequent Stack

Implement the most frequent stack.

Requirements:
1. `push()` pushes the element into the stack.
2. `pop()` remove and get the most frequently element in the stack. Get the one which is closest to the top when there are more than one most frequently element.

```java
public class MostFrequentStack {

    Map<Integer, Integer> freq;
    Map<Integer, Stack<Integer>> group;
    int maxfreq;

    public MostFrequentStack() {
        freq = new HashMap<>();
        group = new HashMap<>();
        maxfreq = 0;
    }

    public void push(int x) {
        int f = freq.getOrDefault(x, 0) + 1;
        freq.put(x, f);
        if (f > maxfreq) {
            maxfreq = f;
        }
        group.computeIfAbsent(f, z -> new Stack<Integer>()).push(x);
    }

    public int pop() {
        int x = group.get(maxfreq).pop();
        freq.put(x, freq.get(x) - 1);
        if (group.get(maxfreq).size() == 0) {
            maxfreq--;
        }
        return x;
    }

    public static void main(String[] args) {
        MostFrequentStack stack = new MostFrequentStack();
        int[] arr = { 5, 7, 5, 7, 4, 5 };
        for (int a : arr) {
            stack.push(a);
        }
        for (int i = 0; i < arr.length; i++) {
            System.out.println(stack.pop());
        }
    }

}

// push: 5, 7, 5, 7, 4, 5
// Output: 5, 7, 5, 4, 7, 5,
```

- The time complexity of `push` and `pop` is `O(1)`.
- The space complexity is `O(N)`. (N is the number of elements in the stack.)

## Question 22: Remove kth-to-last Element in Linked List

Remove the kth-to-last element in a linked list.

Requirements: traverse the list for ONLY ONCE!

Tips: use two pointers. Keep these two pointers within a gap of k and move them together.

- The time complexity is `O(N)`. (N is the number of elements in the list.)
- The space complexity is `O(1)`.

## Question 26: Quality Guarantee for a New Product

1. Code Development: unit test, code review, static code scan.
2. Testing: function test, performance test, high availability test, stress test, stability test, compatibility test.
3. Deployment: gray release, roll back, breakdown simulation, online monitor.

## Question 28: Synchronous Queue

What will happen?

```java
public class SynchronousQueueQuiz {
    public static void main(String[] args) throws Exception {
        BlockingQueue<Integer> queue = new SynchronousQueue<>();
        System.out.print(queue.offer(1) + " ");
        System.out.print(queue.offer(2) + " ");
        System.out.print(queue.offer(3) + " ");
        System.out.print(queue.take() + " ");
        System.out.println(queue.size());
    }
}
```

The answer is: false false false (blocked).

If you want to know more about Blocking Queue or other related information, find the links in the references.


# References

1. [阿里开发者招聘节 \| 2019阿里巴巴技术面试题集锦！参考答案已公布！](https://yq.aliyun.com/articles/699746?utm_content=g_1000054983&scene=126&from=singlemessage){:target="_blank"}
2. [LRU Cache Implementation](https://www.geeksforgeeks.org/lru-cache-implementation/){:target="_blank"}
3. [BlockingQueue (Java Platform SE 8) - Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/BlockingQueue.html){:target="_blank"}
4. [Java BlockingQueue examples By mkyong](https://www.mkyong.com/java/java-blockingqueue-examples/){:target="_blank"}
