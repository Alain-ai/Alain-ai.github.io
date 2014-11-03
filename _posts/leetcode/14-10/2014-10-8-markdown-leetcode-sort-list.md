---
layout: post
title: LeetCode | Sort List in Python
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
    Sort a linked list in O(n log n) time using constant space complexity.

Algorithm:
    merge sort

Note:
    can not get accepted sigh
'''


class Solution:
    # @param head, a ListNode
    # @return a ListNode
    def sortList(self, head):
        if not head or not head.next:
            return head
        p = pp = dummy = ListNode(0)
        dummy.next = head
        while p and pp and pp.next:
            p = p.next
            pp = pp.next.next
        p1, p2 = head, p.next
        p.next = None
        p1 = self.sortList(p1)
        p2 = self.sortList(p2)
        p = dummy = ListNode(0)
        dummy.next = p1
        while p1 and p2:
            if p1.val < p2.val:
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
