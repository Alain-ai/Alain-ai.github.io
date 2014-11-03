---
layout: post
title: LeetCode | Combinations in Python
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
    Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

Algorithm:
    DFS
'''


class Solution:
    # @return a list of lists of integers
    def combine(self, n, k):
        res = []
        self.combine_rec([i for i in xrange(1, n+1)], k, 0, [], res)
        return res

    def combine_rec(self, repo, k, start, stk, res):
        if len(stk) == k:
            res.append(stk)
        else:
            for i in xrange(start, len(repo)):
                self.combine_rec(repo, k, i+1, stk+[repo[i]], res)
</pre>
