---
layout: post
title: LeetCode | Binary Tree Maximum Path Sum in Python
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
    Given a binary tree, find the maximum path sum. The path may start and end at any node in the tree.

Algorithm:
    1. "maxPathSum_rec(node)" returns the path with maximal sum which starts at "node"
    2. "max_local" is the maximal sum of the path which passes by the specific node(root)
    3. we would like to find the max of all "max_local"s among all nodes
'''


class Solution:
    # @param root, a tree node
    # @return an integer
    def maxPathSum(self, root):
        res = [-(1<<31)]
        self.maxPathSum_rec(root, res)
        return res[0]

    def maxPathSum_rec(self, root, res):
        if not root:
            return 0
        max_left = self.maxPathSum_rec(root.left, res)
        max_right = self.maxPathSum_rec(root.right, res)
        max_local = max(max_left, 0) + max(max_right, 0) + root.val
        res[0] = max(res[0], max_local)
        return max(max_left, max_right, 0) + root.val
</pre>
