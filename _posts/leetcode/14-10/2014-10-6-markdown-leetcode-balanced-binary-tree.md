---
layout: post
title: LeetCode | Balanced Binary Tree in Python
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
    Given a binary tree, determine if it is height-balanced. For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Algorithm:
    recursion
    follow the definition
'''


class Solution:
    # @param root, a tree node
    # @return a boolean
    def isBalanced(self, root):
        return self.isBalanced_rec(root)[0]

    def isBalanced_rec(self, root):
        if not root:
            return True, 0
        bal_left, height_left = self.isBalanced_rec(root.left)
        bal_right, height_right = self.isBalanced_rec(root.right)
        return bal_left and bal_right and abs(height_left - height_right) <= 1, max(height_left, height_right) + 1
</pre>
