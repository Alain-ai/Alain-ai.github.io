---
layout: post
title: LeetCode | Reverse Nodes in k-Group in Python
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
    Given a linked list, reverse the nodes of a linked list k at a time and return its modified list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is. You may not alter the values in the nodes, only nodes itself may be changed. Only constant memory is allowed.

Algorithm:
    ...

Note:
    when reversing, set None ahead and behind
'''


class Solution:
    # @param head, a ListNode
    # @param k, an integer
    # @return a ListNode
    def reverseKGroup(self, head, k):
        pp = p = dummy = ListNode(0)
        cnt, p.next = 0, head
        while p.next:
            p, cnt = p.next, cnt + 1
            if cnt % k == 0:
                p_next, pp_next = p.next, pp.next
                p.next = None
                head_rev = self.reverse(pp_next)
                pp.next = head_rev
                pp_next.next = p_next
                pp = p = pp_next
        return dummy.next

    def reverse(self, head):
        if not head or not head.next:
            return head
        p = head.next
        head.next = None
        head_rev = self.reverse(p)
        p.next = head
        return head_rev
</pre>
