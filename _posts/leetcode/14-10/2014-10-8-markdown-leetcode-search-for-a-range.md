---
layout: post
title: LeetCode | Search for a Range in Python
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
    Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order. You may assume no duplicates in the array.

Algorithm:
    binary search
    1. the lower bound finally returns the first index which holds the value no less than the target
    2. the upper bound finally returns the last index which holds the value no more than the target

Note:
    Corner cases:
    1. len(A) <= 1
    2. the target is at the two ends
'''


class Solution:
    # @param A, a list of integers
    # @param target, an integer to be searched
    # @return a list of length 2, [index1, index2]
    def searchRange(self, A, target):
        found = False
        if len(A) == 0:
            return [-1, -1]
        i, j = 0, len(A) - 1
        while i <= j:
            m = (i+j) >> 1
            if A[m] == target:
                found = True
                j -= 1
            elif A[m] < target:
                i = m + 1
            else:
                j = m - 1
        low = i if found else -1
        i, j = 0, len(A) - 1
        while i <= j:
            m = (i + j) >> 1
            if A[m] == target:
                i += 1
            elif A[m] < target:
                i = m + 1
            else:
                j = m - 1
        high = j if found else -1
        return [low, high]
</pre>
