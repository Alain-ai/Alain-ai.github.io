---
layout: post
title: LeetCode | Symmetric Tree in Python
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
    Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

Algorithm:
    DFS
    "isSymmetric_rec(left, right)" returns True when left and its subtree is the same as right and its subtree
'''


class Solution:
    # @param root, a tree node
    # @return a boolean
    def isSymmetric(self, root):
        if not root:
            return False
        return self.isSymmetric_rec(root.left, root.right)

    def isSymmetric_rec(self, left, right):
        if left == right is None:
            return True
        elif left is None or right is None:
            return False
        elif left.val == right.val:
            return self.isSymmetric_rec(left.left, right.right) and self.isSymmetric_rec(left.right, right.left)
        else:
            return False
</pre>
