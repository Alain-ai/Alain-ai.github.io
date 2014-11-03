---
layout: post
title: LeetCode | Sort Colors in Python
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
    Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue. Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively

Algorithm:
    Partition
'''


class Solution:
    # @param A a list of integers
    # @return nothing, sort in place
    def sortColors(self, A):
        l, h, i = 0, len(A) - 1, 0
        while i <= h:
            if A[i] < 1:
                A[l], A[i] = A[i], A[l]
                l += 1
                i += 1
            elif A[i] > 1:
                A[h], A[i] = A[i], A[h]
                h -= 1
            else:
                i += 1
</pre>
