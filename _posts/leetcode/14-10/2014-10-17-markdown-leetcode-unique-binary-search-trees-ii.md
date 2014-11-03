---
layout: post
title: LeetCode | Unique Binary Search Trees II in Python
categories: LeetCode
tags: Python

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
jax: ["input/TeX","output/HTML-CSS"],
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]},
extensions: ["tex2jax.js","MathMenu.js","MathZoom.js"],
TeX: { equationNumbers: { autoNumber: "AMS" }, extensions: ["AMSmath.js", "AMSsymbols.js","noErrors.js","noUndefined.js"]}
});
</script>

<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML">
</script>

<pre>
'''
Question:
    Given n, generate all structurally unique BST\'s (binary search trees) that store values 1...n.

Algorithm:
    recursion
'''


class Solution:
    # @return a list of tree node
    def generateTrees(self, n):
        return self.generateTrees_rec(1, n)

    def generateTrees_rec(self, s, e):
        if s > e:
            return [None]
        res = []
        for i in xrange(s, e+1):
            left_arr, right_arr = self.generateTrees_rec(s, i-1), self.generateTrees_rec(i+1, e)
            for left in left_arr:
                for right in right_arr:
                    root, root.left, root.right = TreeNode(i), left, right
                    res.append(root)
        return res
</pre>
