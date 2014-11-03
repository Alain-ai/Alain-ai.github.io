---
layout: post
title: LeetCode | Remove Nth Node From End of List in Python
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
    Given a linked list, remove the nth node from the end of list and return its head.

Algorithm:
    corner case would be n <= 0 or n > len, but we don\'t have to consider corner cases this time since n is good here

Note:
    1. Given n will always be valid.
    2. Try to do this in one pass.
'''


class Solution:
    # @return a ListNode
    def removeNthFromEnd(self, head, n):
        p = head
        for i in xrange(1, n):
            p = p.next
        dummy = ListNode(0)
        dummy.next = head
        pp = dummy
        while p.next:
            p = p.next
            pp = pp.next
        if pp.next:
            pp.next = pp.next.next
        else:
            pp.next = None
        return dummy.next
</pre>
