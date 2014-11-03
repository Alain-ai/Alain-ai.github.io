---
layout: post
title: LeetCode | Unique Binary Search Trees in Python
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
    Given n, how many structurally unique BST\'s (binary search trees) that store values 1...n?

Algorithm:
    DP
    DP[i] = sum(DP[j] * DP[i-1-j]) over j from 0 to i-1
'''


class Solution:
    # @return an integer
    def numTrees(self, n):
        DP = [1, 1] + [0 for i in xrange(n-1)]
        for i in xrange(2, n+1):
            for j in xrange(i):
                k = i - j - 1
                DP[i] += DP[j] * DP[k]
        return DP[-1]
</pre>
