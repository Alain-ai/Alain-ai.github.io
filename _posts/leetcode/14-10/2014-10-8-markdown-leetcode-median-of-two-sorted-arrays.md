---
layout: post
title: LeetCode | Median of Two Sorted Arrays in Python
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
    There are two sorted arrays A and B of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

Algorithm:
    a variant of binary search
'''


class Solution:
    # @return a float
    def findMedianSortedArrays(self, A, B):
        if len(A) == len(B) == 0:
            return None
        ls = len(A) + len(B)
        if ls & 1:
            return self.find_smallest_k(A, B, 0, 0, ls/2+1)
        else:
            return (self.find_smallest_k(A, B, 0, 0, ls/2) + self.find_smallest_k(A, B, 0, 0, ls/2+1)) / 2.

    def find_smallest_k(self, A, B, sa, sb, kth):
        if len(A) > len(B):
            return self.find_smallest_k(B, A, sb, sa, kth)
        if sa == len(A):
            return B[sb+kth-1]
        if sb == len(B):
            return A[sa+kth-1]
        if kth == 1:
            return min(A[sa], B[sb])
        ca = min(kth/2, len(A) - sa)  # the number of elements "a" can contribute
        cb = kth - ca  # the number of elements "a" can contribute
        if A[sa + ca - 1] == B[sb + cb - 1]:
            return A[sa + ca - 1]
        elif A[sa + ca - 1] > B[sb + cb - 1]:  # B[sb:sb+cb] must be less than the kth element
            return self.find_smallest_k(A, B, sa, sb + cb, kth-cb)
        else:  # A[sa:sa+ca] must be less than the kth element
            return self.find_smallest_k(A, B, sa+ca, sb, kth-ca)
</pre>
