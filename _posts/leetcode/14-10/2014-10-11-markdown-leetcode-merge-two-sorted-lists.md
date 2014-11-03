---
layout: post
title: LeetCode | Merge Two Sorted Lists in Python
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
    Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Algorithm:
    straightforward
'''


class Solution:
    # @param two ListNodes
    # @return a ListNode
    def mergeTwoLists(self, l1, l2):
        p = dummy = ListNode(0)
        p1, p2 = l1, l2
        while p1 and p2:
            if p1.val <= p2.val:
                p.next = p1
                p1 = p1.next
            else:
                p.next = p2
                p2 = p2.next
            p = p.next
        if p1:
            p.next = p1
        if p2:
            p.next = p2
        return dummy.next
</pre>
