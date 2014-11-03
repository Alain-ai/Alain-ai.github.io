---
layout: post
title: LeetCode | Subsets in Python
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
    Given a set of distinct integers, S, return all possible subsets. Elements in a subset must be in non-descending order. The solution set must not contain duplicate subsets.

Algorithm:
    DFS
'''


class Solution:
    # @param S, a list of integer
    # @return a list of lists of integer
    def subsets(self, S):
        res = []
        S.sort(reverse=True)
        self.subsets_rec(S, 0, res)
        return res

    def subsets_rec(self, arr, i, res):
        if i == len(arr):
            res.append([])
        else:
            self.subsets_rec(arr, i+1, res)
            res.extend([item + [arr[i]] for item in res])
</pre>
