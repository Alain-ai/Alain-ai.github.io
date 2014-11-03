---
layout: post
title: LeetCode | Unique Paths II in Python
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
    A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below). The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below). Now consider if some obstacles are added to the grids. How many unique paths would there be? An obstacle and empty space is marked as 1 and 0 respectively in the grid.

Algorithm:
    DP
    initially set "DP" as 0 when there is an obstacle
'''


class Solution:
    # @param obstacleGrid, a list of lists of integers
    # @return an integer
    def uniquePathsWithObstacles(self, obstacleGrid):
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        DP = [[1-cell for cell in row] for row in obstacleGrid]
        for i in xrange(0, m):
            for j in xrange(0, n):
                if not obstacleGrid[i][j]:
                    DP[i][j] = 1 if i == j == 0 else (DP[i-1][j] if i > 0 else 0) + (DP[i][j-1] if j > 0 else 0)
        return DP[m-1][n-1]
</pre>
