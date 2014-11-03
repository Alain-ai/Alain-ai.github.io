---
layout: post
title: LeetCode | Minimum Depth of Binary Tree in Python
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
    Given a binary tree, find its minimum depth. The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Algorithm:
    Recursion
    get min when it comes to a leaf node
'''


class Solution:
    # @param root, a tree node
    # @return an integer
    def minDepth(self, root):
        if not root:
            return 0
        res = [1 << 31]
        self.minDepth_rec(self, root, 1, res)
        return res[0]

    def minDepth_rec(self, root, level, min_depth):
        if not root:
            return
        if not root.left and not root.right:
            min_depth[0] = min(min_depth[0], level)
        self.minDepth_rec(root.left, level+1, min_depth)
        self.minDepth_rec(root.right, level+1, min_depth)
</pre>
