---
layout: post
title: Vector vs SynchronizedList
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

This post is aiming to extend the discussion [here](http://stackoverflow.com/questions/14932034/in-java-vector-and-collections-synchronizedlist-are-all-synchronized-whats-ths).
In java, Vector and Collections.synchronizedList are all synchronized randomly-accessable lists. For historical reasons, this redundancy exists and is reserved until now. How are they different from each other?

## Differences

The main difference between them is how the underlying data is stored.

Collections.synchronizedList is a wrapper class around your current List implementation, which means you don't copy data to another data structure and you keep underlying structure intact.

<pre>
public static <T> List<T> synchronizedList(List<T> list) {

    return (list instanceof RandomAccess ? new SynchronizedRandomAccessList<T>(list) :
        new SynchronizedList<T>(list));
}

static class SynchronizedList<E> extends SynchronizedCollection<E> implements List<E> {

    private static final long serialVersionUID = -7754090372962971524L;

    final List<E> list;

    SynchronizedList(List<E> list) {
        super(list);
        this.list = list;
    }

    // other staff
    ....

}
</pre>

The idea is implemented at line 15. Line 14 ensures the synchronization at the superclass SynchronizedCollection. We are able to use all APIs provided by List<E> Interface in a thread-safe way because synchronizedList implements List<E>.

In case of a Vector, it actually holds the data internally. So if you want to take Vector as a wrapper of Arraylist to obtain synchronization, it would less efficient because it will make a copy of data. Another disadvantage of a Vector object is that it's an instance of RandomAccess Interface and therefore if a Vector object wraps a non-RandomAccess list like LinkedList, LinkedList will copy its values to an array by calling toArray method as shown at line 2. Thus the underlying LinkedList object loses its properties.

<pre>
public Vector(Collection<? extends E> c) {

    elementData = c.toArray();
    elementCount = elementData.length;
    // c.toArray might (incorrectly) not return Object[] (see 6260652)
    if (elementData.getClass() != Object[].class)
        elementData = Arrays.copyOf(elementData, elementCount, Object[].class);
}
</pre>

The wrapper synchronizedList is going to equip a list. It wraps not only a RandomAccess list like ArrayList but also a sequential-access list like LinkedList.

<pre>
public static <T> List<T> synchronizedList(List<T> list) {

    return (list instanceof RandomAccess ? new SynchronizedRandomAccessList<T>(list) :
        new SynchronizedList<T>(list));
}
</pre>

In addition to SynchronizedList, java.util.Collections also offers more synchronized wrappers such as

1. synchronizedCollection
2. synchronizedMap
3. synchronizedSet
4. synchronizedSortedMap
5. synchronizedSortedSet

where synchronizedCollection is the superclass of all others.
