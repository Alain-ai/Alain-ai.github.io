---
layout: post
title: LeetCode | Search a 2D Matrix in Python
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
    Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
    1. Integers in each row are sorted from left to right.
    2. The first integer of each row is greater than the last integer of the previous row.

Algorithm:
    a variant of binary search
    consider the storage of this matrix, it is actually a long array that ars split into pieces
    we can think we are operating this long array conceptually
    the only thing we need here is the coordinate solving system which is as simple as division and mod operations
'''


class Solution:
    # @param matrix, a list of lists of integers
    # @param target, an integer
    # @return a boolean
    def searchMatrix(self, matrix, target):
        if len(matrix) == 0:
            return False
        m, n = len(matrix), len(matrix[0])
        s, e = 0, m*n - 1
        while s <= e:
            mid = (s+e) >> 1
            x, y = mid / n, mid % n
            if matrix[x][y] == target:
                return True
            elif matrix[x][y] < target:
                s += 1
            else:
                e -= 1
        return False
</pre>
