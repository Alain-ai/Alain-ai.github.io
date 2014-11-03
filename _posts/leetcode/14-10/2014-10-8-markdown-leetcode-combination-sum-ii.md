---
layout: post
title: LeetCode | Combination Sum II in Python
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
    Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T. Each number in C may only be used once in the combination.

Note:
    1. All numbers (including target) will be positive integers.
    2. Elements in a combination (a1, a2, ... , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ ... ≤ ak).
    3. The solution set must not contain duplicate combinations.

Algorithm:
    DFS
    when candidates[i] == candidates[i-1], ignore candidates[i] to avoid duplications
'''


class Solution:
    # @param candidates, a list of integers
    # @param target, integer
    # @return a list of lists of integers
    def combinationSum2(self, candidates, target):
        res = []
        candidates.sort()
        self.combinationSum2_rec(candidates, target, 0, [], res)
        return res

    def combinationSum2_rec(self, candidates, target, start, stk, res):
        if target == 0:
            res.append(stk)
        if target > 0:
            for i in xrange(start, len(candidates)):
                if i > start and candidates[i] == candidates[i-1]:
                    continue
                self.combinationSum2_rec(candidates, target-candidates[i], i+1, stk+[candidates[i]], res)
</pre>
