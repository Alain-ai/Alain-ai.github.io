---
layout: post
title: LeetCode | Search in Rotated Sorted Array in Python
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
    (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2). You are given a target value to search. If found in the array return its index, otherwise return -1. You may assume no duplicate exists in the array.

Algorithm:
    binary search
    1. A[i] <= A[mid] < target, -->
    2. target <= A[j] and not target < A[mid] <= A[j], -->
    3. else <--
'''


class Solution:
    # @param A, a list of integers
    # @param target, an integer to be searched
    # @return an integer
    def search(self, A, target):
        i, j = 0, len(A) - 1
        while i <= j:
            mid = (i + j) >> 1
            if A[mid] == target:
                return mid
            elif A[i] <= A[mid] < target or (target <= A[j] and not target < A[mid] <= A[j]):
                i += 1
            else:
                j -= 1
            # if A[mid] >= A[i]:
            #     if A[i] <= target < A[mid]:
            #         j -= 1
            #     else:
            #         i += 1
            # else:
            #     if A[mid] < target <= A[j]:
            #         i += 1
            #     else:
            #         j -= 1
        return -1
</pre>
