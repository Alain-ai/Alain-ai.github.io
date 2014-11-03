---
layout: post
title: LeetCode | Remove Duplicates from Sorted Array II in Python
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
    Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length. Do not allocate extra space for another array, you must do this in place with constant memory. What if duplicates are allowed at most twice?

Algorithm:
    ...
'''


class Solution:
    # @param A a list of integers
    # @return an integer
    def removeDuplicates(self, A):
        if len(A) == 0:
            return 0
        repeated, idx = False, 1
        for i in xrange(1, len(A)):
            if A[i-1] == A[i]:
                repeated = True
            else:
                if repeated:
                    A[idx] = A[i-1]
                    idx += 1
                    A[idx] = A[i]
                    idx += 1
                else:
                    A[idx] = A[i]
                    idx += 1
                repeated = False
        if repeated:
            A[idx] = A[-1]
            idx += 1
        return idx
</pre>
