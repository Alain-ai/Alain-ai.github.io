---
layout: post
title: LeetCode | Search in Rotated Sorted Array II in Python
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
    Suppose a sorted array is rotated at some pivot unknown to you beforehand.
    (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2). You are given a target value to search. What if duplicates are allowed? Would this affect the run-time complexity? How and why? Write a function to determine if a given target is in the array.

Algorithm:
    binary search
    1. A[mid] == A[i], -->
    2. A[i] <= A[mid] < target, -->
    3. target <= A[j] and not target < A[mid] <= A[j], -->
    4. else <--
'''


class Solution:
    # @param A a list of integers
    # @param target an integer
    # @return a boolean
    def search(self, A, target):
        i, j = 0, len(A) - 1
        while i <= j:
            mid = (i + j) >> 1
            if A[mid] == target:
                return True
            if A[mid] == A[i]:
                i += 1
                continue
            if A[i] < A[mid] < target or (target <= A[j] and not target < A[mid] <= A[j]):
                i += 1
            else:
                j -= 1
        return False
</pre>
