---
layout: post
title: LeetCode | Sum Root to Leaf Numbers in Python
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
    Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number. An example is the root-to-leaf path 1->2->3 which represents the number 123. Find the total sum of all root-to-leaf numbers. For example,

    1
   / \
  2   3
    The root-to-leaf path 1->2 represents the number 12. The root-to-leaf path 1->3 represents the number 13. Return the sum = 12 + 13 = 25.

Algorithm:
    "tmp" stores the value from the upper layers, times 10 and plus the value of the current node
'''


class Solution:
    # @param root, a tree node
    # @return an integer
    def sumNumbers(self, root):
        if not root:
            return 0
        res = [0]
        self.sumNumbers_rec(root, 0, res)
        return res[0]

    def sumNumbers_rec(self, root, tmp, res):
        tmp = tmp * 10 + root.val
        if not root.left and not root.right:
            res[0] += tmp
            return
        if root.left:
            self.sumNumbers_rec(root.left, tmp, res)
        if root.right:
            self.sumNumbers_rec(root.right, tmp, res)
</pre>
