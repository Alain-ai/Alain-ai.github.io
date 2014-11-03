---
layout: post
title: LeetCode | Combination Sum in Python
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
    Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T. The same repeated number may be chosen from C unlimited number of times.

Note:
    1. All numbers (including target) will be positive integers.
    2. Elements in a combination (a1, a2, ... , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ ... ≤ ak).
    3. The solution set must not contain duplicate combinations.

Algorithm:
    DFS
'''


class Solution:
    # @param candidates, a list of integers
    # @param target, integer
    # @return a list of lists of integers
    def combinationSum(self, candidates, target):
        res = []
        candidates.sort()
        self.combinationSum_rec(candidates, target, 0, [], res)
        return res

    def combinationSum_rec(self, candidates, target, start, stk, res):
        if target == 0:
            res.append(stk)
        if target > 0:
            for i in xrange(start, len(candidates)):
                self.combinationSum_rec(candidates, target-candidates[i], i, stk+[candidates[i]], res)
</pre>
