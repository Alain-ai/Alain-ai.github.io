---
layout: post
title: Shallow & Deep Copy
categories: Language
tags: Python

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>


## Shallow Copy

### Operaitons
In python, an operation of shallow copy is as follows:
<pre>
a = [...]
b = a[:]
b = list(a)
###########
a = {...}
b = dict(a)
###########
import copy
b = copy.copy(a)
</pre>

### Principles
For a compound structure like list, dict or even user-define class, the shallow copy will just go through the first level in the structure. Specifically, it iterates over all fields in that structure, if a field is a simple structure(like an integer), a copy of the value will be made; on the other hand, if a field is a compound structure, only the reference is going to be copyed.

### Example
Here is an example to illustrate.
<pre>
l1 = [1, [2,3], [4,5]]
l2 = l1[:] # l2 = list(l1) is identical
l2[0] = 6
print l1 # [1, [2,3], [4,5]]
print l2 # [6, [2,3], [4,5]]
l2[1] = [7, 8]
print l1 # [1, [2,3], [4,5]]
print l2 # [6, [7,8], [4,5]]
# the 2nd reference in l2 that was pointing to [2,3] is now to [7,8], [2,3] in l1 remains
l2[2][0] = 9
print l1 # [1, [2,3], [9,5]]
print l2 # [6, [7,8], [9,5]]
# 3rd reference in l1 and l2 was pointing to the same memory, [4,5], then the memory gets change to [9,5], l1 is affected
</pre>

## Deep Copy
### Operaitons
In python, an operation of shallow copy is as follows:
<pre>
import copy
b = copy.deepcopy(a)
</pre>

### Principles
For a compound structure, the deep copy will go throught all the way to the bottom level of the structure and construct a new compound object and then, recursively, inserts copies into it of the objects found in the original.

### Example
Here is an example to illustrate.
<pre>
import copy
l1 = [1, [2,3], [4,5]]
l2 = copy.deepcopy(l1)
l2[0] = 6
print l1 # [1, [2,3], [4,5]]
print l2 # [6, [2,3], [4,5]]
l2[1] = [7, 8]
print l1 # [1, [2,3], [4,5]]
print l2 # [6, [7,8], [4,5]]
l2[2][0] = 9
print l1 # [1, [2,3], [4,5]]
print l2 # [6, [7,8], [9,5]]
</pre>
