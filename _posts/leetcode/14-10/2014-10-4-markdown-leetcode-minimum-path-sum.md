---
layout: post
title: LeetCode | Minimum Path Sum in Python
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
    Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Algorithm:
    DP
    f(i, j) = min(f(i-1, j), f(i, j-1)) + val(i, j)
'''


class Solution:
    # @param grid, a list of lists of integers
    # @return an integer
    def minPathSum(self, grid):
        if len(grid) == 0:
            return 0
        m, n = len(grid), len(grid[0])
        DP = [[cell for cell in row] for row in grid]
        for i in xrange(m):
            for j in xrange(n):
                if not i == j == 0:
                    DP[i][j] = min((DP[i-1][j] if i > 0 else 1<<31), (DP[i][j-1] if j > 0 else 1<<31)) + grid[i][j]
        return DP[m-1][n-1]
</pre>
