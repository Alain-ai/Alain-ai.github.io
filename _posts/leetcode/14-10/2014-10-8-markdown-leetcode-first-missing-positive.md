---
layout: post
title: LeetCode | First Missing Positive in Python
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
    Given an unsorted integer array, find the first missing positive integer. For example,
    Given [1,2,0] return 3, and [3,4,-1,1] return 2. Your algorithm should run in O(n) time and uses constant space.

Algorithm:
    1. if A[i] <= 0, ignore
    2. if A[i] > len(A), ignore
    3. otherwise try to let A[i] = i + 1 by exchanging

Note:
    Corner cases:
        1. len(A) == 0
        2. A = [1]
        3. A = [-1]
        4. A = [2]
'''


class Solution:
    # @param A, a list of integers
    # @return an integer
    def firstMissingPositive(self, A):
        i = 0
        while i < len(A):
            if 1 <= A[i] <= len(A) and A[A[i]-1] != A[i]:
                A[A[i]-1], A[i] = A[i], A[A[i]-1]
            else:
                i += 1
        i = 0
        while i < len(A):
            if A[i] != i+1:
                return i+1
            i += 1
        return i+1
</pre>
