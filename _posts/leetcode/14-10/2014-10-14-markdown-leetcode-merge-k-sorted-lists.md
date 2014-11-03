---
layout: post
title: LeetCode | Merge k Sorted Lists in Python
categories: LeetCode
tags: Python

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>


<pre>
'''
Question:
    Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Algorithm:
    min-heap to store k heads of all lists
'''


class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

    def __repr__(self):
        return str(self.val)

    def lt(self, other):
        return self.val < other.val


class Solution:
    # @param a list of ListNode
    # @return a ListNode
    def mergeKLists(self, lists):
        lists = filter(lambda x: x is not None, lists)
        heads = map(lambda x: (x.val, x), lists)
        heapq.heapify(heads)
        p = dummy = ListNode(0)
        while heads:
            val, node = heapq.heappop(heads)
            p.next, p = node, node
            if node.next:
                heapq.heappush(heads, (node.next.val, node.next))
        return dummy.next
</pre>
