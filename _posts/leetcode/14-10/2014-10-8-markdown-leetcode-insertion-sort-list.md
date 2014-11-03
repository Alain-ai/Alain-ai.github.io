---
layout: post
title: LeetCode | Insertion Sort List in Python
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
    Sort a linked list using insertion sort.

Algorithm:
    ...

Note:
    Can not get accepted sigh...
'''


class Solution:
    # @param head, a ListNode
    # @return a ListNode
    def insertionSortList(self, head):
        p = dummy = ListNode(head.val)
        dummy.next = head
        while p.next:
            if p.next.val >= p.val:
                p = p.next
            else:
                tmp = p.next
                p.next = tmp.next
                pp = dummy
                while pp.next and pp != p:
                    if pp.next.val > tmp.val:
                        tmp.next = pp.next
                        pp.next = tmp
                        break
                    else:
                        pp = pp.next
        return dummy.next
</pre>
