---
layout: post
title: LeetCode | 3Sum Closest in Python
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
    Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

Algorithm:
    fix one and approach from two sides to the middle
'''


class Solution:
    # @return an integer
    def threeSumClosest(self, num, target):
        num = sorted(num)
        res, min_diff = 0, 1 << 31
        for i in xrange(len(num)):
            j, k = i + 1, len(num) - 1
            while j < k:
                diff = target - (num[i] + num[j] + num[k])
                if abs(diff) < min_diff:
                    res, min_diff = num[i] + num[j] + num[k], abs(diff)
                if diff > 0:
                    j += 1
                elif diff < 0:
                    k -= 1
                else:
                    return num[i] + num[j] + num[k]
        return res
</pre>
