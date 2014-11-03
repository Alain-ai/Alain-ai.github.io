---
layout: post
title: LeetCode | Partition List in Python
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
    Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x. You should preserve the original relative order of the nodes in each of the two partitions.

Algorithm:
    DFS
    a node in the original list will be send to one of two new lists, one of which contains nodes less than x and the other one contains others.
'''


class Solution:
    # @param head, a ListNode
    # @param x, an integer
    # @return a ListNode
    def partition(self, head, x):
        p1 = dummy1 = ListNode(0)
        p2 = dummy2 = ListNode(0)
        p = head
        if not head:
            return head
        while p:
            if p.val < x:
                p1.next = p
                p1 = p
            else:
                p2.next = p
                p2 = p
            p = p.next
        p1.next = dummy2.next
        return dummy1.next
</pre>
