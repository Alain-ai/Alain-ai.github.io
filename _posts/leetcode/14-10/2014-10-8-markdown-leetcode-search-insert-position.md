---
layout: post
title: LeetCode | Search Insert Position in Python
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
    3. we use "1" here

Note:
    Corner cases:
    1. len(A) <= 1
    2. the insertion place is at the two sides
'''


class Solution:
    # @param A, a list of integers
    # @param target, an integer to be inserted
    # @return integer
    def searchInsert(self, A, target):

        if len(A) == 0:
            return 0
        i, j = 0, len(A) - 1
        while i <= j:
            m = (i+j) >> 1
            if A[m] == target:
                return m
            elif A[m] < target:
                i = m + 1
            else:
                j = m - 1
        return i
</pre>
