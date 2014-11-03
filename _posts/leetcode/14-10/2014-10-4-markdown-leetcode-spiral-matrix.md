---
layout: post
title: LeetCode | Spiral Matrix in Python
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
    Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

Algorithm:
    set two row poniter and two column pointers, let them move forward to each other
'''


class Solution:
    # @param matrix, a list of lists of integers
    # @return a list of integers
    def spiralOrder(self, matrix):
        mat = matrix
        res = []
        if len(matrix) == 0:
            return res
        r, c = len(matrix), len(matrix[0])
        c1, c2 = 0, c - 1
        r1, r2 = 0, r - 1
        while c1 <= c2 and r1 <= r2:
            for i in xrange(c1, c2+1):
                res.append(mat[r1][i])
            r1 += 1
            if c1 > c2 or r1 > r2:
                break
            for i in xrange(r1, r2+1):
                res.append(mat[i][c2])
            c2 -= 1
            if c1 > c2 or r1 > r2:
                break
            for i in xrange(c2, c1-1, -1):
                res.append(mat[r2][i])
            r2 -= 1
            if c1 > c2 or r1 > r2:
                break
            for i in xrange(r2, r1-1, -1):
                res.append(mat[i][c1])
            c1 += 1
            if c1 > c2 or r1 > r2:
                break
        return res
</pre>
