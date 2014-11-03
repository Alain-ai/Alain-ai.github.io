---
layout: post
title: LeetCode | Add Two Numbers in Python
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
    You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Algorithm:
    straightforward
    use one more list to store the result
'''


class Solution:
    # @return a ListNode
    def addTwoNumbers(self, l1, l2):
        carry = 0
        dummy = ListNode(0)
        p1, p2, p3 = l1, l2, dummy
        while p1 and p2:
            tmp = p1.val + p2.val + carry
            carry = tmp / 10
            p3.next = ListNode(tmp % 10)
            p1, p2, p3 = p1.next, p2.next, p3.next
        while p1:
            tmp = p1.val + carry
            carry = tmp / 10
            p3.next = ListNode(tmp % 10)
            p1, p3 = p1.next, p3.next
        while p2:
            tmp = p2.val + carry
            carry = tmp / 10
            p3.next = ListNode(tmp % 10)
            p2, p3 = p2.next, p3.next
        if carry:
            p3.next = ListNode(carry)
        return dummy.next
</pre>
