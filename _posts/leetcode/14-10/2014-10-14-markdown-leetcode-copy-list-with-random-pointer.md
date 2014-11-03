---
layout: post
title: LeetCode | Copy List with Random Pointer in Python
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
    A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null. Return a deep copy of the list.

Algorithm:
    a version without using extra space
'''


class Solution:
    # @param head, a RandomListNode
    # @return a RandomListNode
    def copyRandomList(self, head):
        p = head
        while p:
            p_new = RandomListNode(p.label)
            p_new.next = p.next
            p_new.random = p.random
            p.next = p_new
            p = p_new.next
        p = head
        while p and p.next:
            if p.random:
                p.next.random = p.next.random.next
            p = p.next.next
        p_new = dummy = RandomListNode(0)
        p = head
        while p and p.next:
            tmp = p.next
            p.next = tmp.next
            p_new.next = tmp
            p_new = p_new.next
            p = tmp.next
        return dummy.next
</pre>
