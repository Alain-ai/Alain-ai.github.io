---
layout: post
title: Vector vs ArrayList
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

There are some similarities and differences between java.util.Vector and java.util.ArrayList. We're going to discuss them here. Despite of what has been discussed extensively [here](http://stackoverflow.com/questions/2986296/what-are-the-differences-between-arraylist-and-vector), we still want to talk about it more together with the java source code.

## Similarities

1. They extend and implement the same superclass(AbstractList) and interfaces(List<E>, RandomAccess, Cloneable, java.io.Serializable)
<pre>
public class Vector<E> extends AbstractList<E>, implements List<E>, RandomAccess, Cloneable, java.io.Serializable

public class ArrayList<E> extends AbstractList<E>, implements List<E>, RandomAccess, Cloneable, java.io.Serializable
</pre>

which guarantee that they have the same APIs.
2. They are both resizable implementation of the List interface.

## Differences

1. Thread-safe Or Not
2. Data Growth Methods

### Synchronization
Vectors are synchronized, ArrayLists are not.
Methods which [modifies the list either structurally or simply modifies an element](http://stackoverflow.com/questions/2986296/what-are-the-differences-between-arraylist-and-vector) will be synchronized. In Vectors, all methods has been synchronized. While in Arraylist, none of methods are like that.


### Data Growth

Both the ArrayList and Vector will expand their underlying arrays internally when necessary. A Vector doubles the size of its array, while the ArrayList increases its array size by half.
<pre>
// Vector
private void ensureCapacityHelper(int minCapacity) {
    int oldCapacity = elementData.length;
    if (minCapacity > oldCapacity) {
        Object[] oldData = elementData;
        int newCapacity = (capacityIncrement > 0) ?
            (oldCapacity + capacityIncrement) : (oldCapacity * 2);
        if (newCapacity < minCapacity) {
            newCapacity = minCapacity;
        }
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
}

// ArrayList
public void ensureCapacity(int minCapacity) {
    modCount++;
    int oldCapacity = elementData.length;
    if (minCapacity > oldCapacity) {
        Object oldData[] = elementData;
        int newCapacity = (oldCapacity * 3)/2 + 1;
        if (newCapacity < minCapacity)
            newCapacity = minCapacity;
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
}
</pre>
