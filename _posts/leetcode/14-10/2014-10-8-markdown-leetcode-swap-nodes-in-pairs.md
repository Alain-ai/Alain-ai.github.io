---
layout: post
title: LeetCode | Swap Nodes in Pairs in Python
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
    Given a linked list, swap every two adjacent nodes and return its head.

Algorithm:
    ...
'''


class Solution:
    # @param a ListNode
    # @return a ListNode
    def swapPairs(self, head):
        dummy = ListNode(0)
        dummy.next, p = head, dummy
        while p.next and p.next.next:
            p1, p2 = p.next, p.next.next
            p.next = p2
            p1.next = p2.next
            p2.next = p1
            p = p1
        return dummy.next
</pre>
