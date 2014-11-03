---
layout: post
title: LeetCode | Path Sum II in Python
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
    Given a binary tree and a sum, find all root-to-leaf paths where each path\'s sum equals the given sum.

    For example:
    Given the below binary tree and sum = 22,
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
    return
    [
       [5,4,11,2],
       [5,8,4,5]
    ]

Algorithm:
    Recursion
'''


class Solution:
    # @param root, a tree node
    # @param sum, an integer
    # @return a list of lists of integers
    def pathSum(self, root, sum):
        res = []
        self.pathSum_rec(root, sum, res, [])
        return res

    def pathSum_rec(self, root, sum, res, path):
        if not root:
            return False
        if not root.left and not root.right:
            if root.val == sum:
                res.append(path + [root.val])
        self.pathSum_rec(root.left, sum - root.val, res, path + [root.val])
        self.pathSum_rec(root.right, sum - root.val, res, path + [root.val])</pre>
