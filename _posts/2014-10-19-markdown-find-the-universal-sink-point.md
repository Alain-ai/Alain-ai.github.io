---
layout: post
title: Find the Universal Sink Vertex
categories: Algorithm
tags: Other

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>

A universal sink vertex in a directed graph is the vertex to which all other vertices point and it points to none of others. So the question is how to find the universal sink vertex if there exists one or declare "No one" otherwise.

Assume the graph has n vertices and m edges. A trivial answer is to detect n vertices one by one and for each one of them, we check if all others point to that and the out-degree of that one is 0. It's obvious that the time complexity is O(n^2).

Let's try to make some improvements by showing an observation. We take two arbitrary vertices out denoted as v and w and then how edges between them are distributed will lie in one of three following situations:

1. v -->w and w --> v, neither of them will be the universal sink
1. v --> w and not w --> v, v won't be
2. w --> v and not v --> w, w won't be
3. no edges between, neither of them will be

Based on this observation, we can find why the aforementioned method is inefficient. Say if we have found that v won't be the universal sink by observing (2, v --> w and not w --> v). Then there is no need for v to take any further detections. In this way we can save some computations.

Here is the pseudo-code.
<pre>
head = list of n vertices
table = adjacency look-up table
p1 = head
p2 = head.next
while p1 and p2:
    if p1 --> p2: # from table
        delete p1
    if p2 --> p1: # from table
        delete p2
    if not (p1 --> p2 or p2 --> p1): # from table
        delete p1 and p2
    reassign head
    p1 = head
    p2 = head.next
</pre>

Finally there might be at most one vertex in the list. If there is one, check if that one is what we want. Otherwise, if the list is empty, it implies there does not exist a universal sink vertex.
