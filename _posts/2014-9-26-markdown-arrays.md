---
layout: post
title: Java Source Code - Arrays
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

Arrays is a tool class to perform operations on array. Roughly speaking, it contains the following methods:

1. sort: QuickSort for primitive type; other types(Object) are sorted by TimSort
2. copy: copyOf and copyOfRange
they actually call System.arraycopy to do the real work
System.arraycopy is a native method that is supposed to be faster than copying position by position
3. binarySearch: regular one as follows:
	- it assumes array has been sorted before calling binarySearch
	<pre>
       int low = fromIndex;  
       int high = toIndex - 1;  
       while (low <= high) {  
         int mid = (low + high) >>> 1;  
         int midVal = a[mid];  
         if (midVal < key)  
           low = mid + 1;  
         else if (midVal > key)  
           high = mid - 1;  
         else  
           return mid; // key found  
       }
       return -(low + 1); // key not found.
    </pre>

4. equals: shallow check, just check elements in the first level
5. deepEquals: deep check, go deep inside until finding a element that is applicable to equals
6. fill: fill the whole array or a sub sequence by a value
	- it's done position by position, no magic here
7. hashcode and toString: iterate over elements
	- hashcode also has deep and shallow versions
