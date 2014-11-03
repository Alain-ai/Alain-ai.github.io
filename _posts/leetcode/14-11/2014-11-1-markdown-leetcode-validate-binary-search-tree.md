---
layout: post
title: LeetCode | Validate Binary Search Tree in Python
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
    Given a binary tree, determine if it is a valid binary search tree (BST). Assume a BST is defined as follows:
    The left subtree of a node contains only nodes with keys less than the node\'s key.
    The right subtree of a node contains only nodes with keys greater than the node\'s key.
    Both the left and right subtrees must also be binary search trees.

Algorithm:
    set min and max for every subtree
'''


class Solution:
    # @param root, a tree node
    # @return a boolean
    def isValidBST(self, root):
        return self.isValidBST_rec(root, -(1<<31), 1<<31)

    def isValidBST_rec(self, root, minv, maxv):
        if not root:
            return True
        elif minv < root.val < maxv:
                return self.isValidBST_rec(root.left, minv, root.val) and self.isValidBST_rec(root.right, root.val, maxv)
        return False
</pre>
