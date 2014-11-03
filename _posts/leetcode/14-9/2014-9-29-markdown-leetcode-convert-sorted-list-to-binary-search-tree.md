---
layout: post
title: LeetCode | Convert Sorted List to Binary Search Tree in Python
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
    Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

Algorithm:
    recursion
    take the middle one as root
    head(inclusive) to the middle one(exclusive) as the left subtree
    the middle one(exclusive) to tail(inclusive) as the right subtree
'''


class Solution:
    # @param head, a list node
    # @return a tree node
    def sortedListToBST(self, head):
        if not head:
            return None
        elif not head.next:
            return TreeNode(head.val)
        dummy = ListNode(0)
        dummy.next = head
        p, pp = dummy
        while p.next and pp.next and pp.next.next:
            p, pp = p.next, pp.next.next
        root = TreeNode(p.next.val)
        head2 = p.next.next
        p.next = None
        left = self.sortedListToBST(head)
        right = self.sortedListToBST(head2)
        root.left = left
        root.right = right
        return root
</pre>
