---
layout: post
title: LeetCode | Rotate Image in Python
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
    You are given an n x n 2D matrix representing an image. Rotate the image by 90 degrees (clockwise).

Algorithm:
    1. transpose the matrix anti-diagonally
    2. exchange rows

Note:
    If transpose the matrix diagonally in the first place, then we have to exchange columns.
    Exchanging columns is less efficient than doing rows because we only exchange references for rows instead of values for columns
'''


class Solution:
    # @param matrix, a list of lists of integers
    # @return a list of lists of integers
    def rotate(self, matrix):
        # matrix transpose first and then exchange columns
        l = len(matrix)
        for i in xrange(0, l - 1):
            for j in xrange(l - 1 - i):
                matrix[i][j], matrix[l-1-j][l-1-i] = matrix[l-1-j][l-1-i], matrix[i][j]
        i, j = 0, l - 1
        while i < j:
            matrix[i], matrix[j] = matrix[j], matrix[i]
            i, j = i + 1, j - 1
        return matrix
</pre>
