---
layout: post
title: LeetCode | Remove Duplicates from Sorted List II in Python
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
    Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

Algorithm:
    straightforward
    use dummy to avoid recording the previous node
    "del_cur" flags whether we have to delete the current node
    note that we should deal with the tail element when "del_cur" is True after we finish the main loop
'''


class Solution:
    # @param head, a ListNode
    # @return a ListNode
    def deleteDuplicates(self, head):
        if not head:
            return head
        dummy = p = ListNode(head.val-1)
        p.next = head
        del_cur = False
        while p.next and p.next.next:
            if p.next.val == p.next.next.val:
                del_cur = True
                p.next.next = p.next.next.next
            else:
                if del_cur:
                    p.next = p.next.next
                    del_cur = False
                    continue
                del_cur = False
                p = p.next
        if del_cur and p and p.next:
            p.next = p.next.next
        return dummy.next
</pre>
