---
layout: post
title: Stack vs LinkedList vs ArrayDeque
categories: Language
tags: Java

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>


This post extends discussion [here](http://stackoverflow.com/questions/6129805/what-is-the-fastest-java-collection-with-the-basic-functionality-of-a-queue) and JavaDocs.

## Stack
Java.util.Stack(short as "Stack") encodes a very basic concept in Computer Science - "stack". "Stack" actually extends Java.util.Vector instead of Java.util.ArrayList, which is unexpected.

<pre>
public Stack<E> extends Vector<E>
</pre>

As a consequence, "Stack" is synchronized, which causes hidden inefficiency when people use it without knowing the fact. But JavaDocs have already suggested a replacement of "Stack". From "Stack"'s' Javadocs:


__A more complete and consistent set of LIFO stack operations is provided by the Deque interface and its implementations, which should be used in preference to this class. For example:__

__Deque<Integer> stack = new ArrayDeque<Integer>();__

## LinkedList
Java.util.LinkedList(short as "LinkedList") encodes doubly linked list concept by implements the interface of Deque. In addition to that, it also provides accessibility like an Random List(pesudo-random) by implementing the List interface.

<pre>
public class LinkedList<E> extends AbstractSequentialList<E> implements List<E>, Deque<E>, Cloneable, java.io.Serializable
</pre>

## ArrayDeque
Java.util.ArrayDeque(short as "ArrayDeque") is an implementation of the Deque interface based on Array.

<pre>
public class ArrayDeque<E> extends AbstractCollection<E> implements Deque<E>, Cloneable, Serializable
</pre>

Just as ArrayList, it has no capacity restrictions thanks to its resizable-array implementation. The underlying array grows as necessary to support usage. This class is likely to be faster than

1. "Stack" when used as a stack. Because "Stack" is synchronized while "ArrayDeque" is not.

2. "LinkedList" when used as a queue. Because ArrayDeque doesn’t have the overhead of node allocations that LinkedList.

3. ArrayList-based Stack when used as a stack. Because "ArrayDeque" maintains a conceptually circular array who won't suffer form the overhead of shifting the array contents left on removal that ArrayList has.


__Note that__ when we are planning to use an array-based List, such as ArrayList, Stack and even ArrayDeque, it would be best practice to estimate the maximal number of elements that might be inserted into. Then when initializing such an instance, we assign enough space in advance so as to avoid the overhead to extend its underlying array during insertions.
