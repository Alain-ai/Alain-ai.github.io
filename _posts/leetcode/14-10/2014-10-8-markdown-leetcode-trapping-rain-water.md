---
layout: post
title: LeetCode | Trapping Rain Water in Python
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
    Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

Algorithm:
    the amount of water trapped at bar i is affected by the highest bars on the left and right
    denote them as "height_i", "high_left", "high_right"
    the amount of water can be hold at bar i is min(high_left, high_right) - height_i
'''


class Solution:
    # @param A, a list of integers
    # @return an integer
    def trap(self, A):
        # corner case:
        # 1. len(A) <= 2
        # 2. same heights for all bars
        max_from_left = [0 for itr in xrange(len(A))]
        max_left = 0
        for i in xrange(len(A)-1, -1, -1):
            if A[i] > max_left:
                max_left = A[i]
            max_from_left[i] = max_left
        max_from_right = [0 for itr in xrange(len(A))]
        max_right = 0
        for i in xrange(len(A)):
            if A[i] > max_right:
                max_right = A[i]
            max_from_right[i] = max_right
        return sum(map(lambda x: min(x[0], x[1]) - x[2], zip(max_from_left, max_from_right, A)))
</pre>
