---
layout: post
title: LeetCode | Spiral Matrix II in Python
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
    Given an integer n, generate a square matrix filled with elements from 1 to n^2 in spiral order.

Algorithm:
    set two row pointer and two column pointers, let them move forward to each other
'''


class Solution:
    # @return a list of lists of integer
    def generateMatrix(self, n):
        r1, r2, c1, c2 = 0, n-1, 0, n-1
        num = 1
        res = [[0 for itr in xrange(n)] for itr2 in xrange(n)]
        while r1 <= r2 and c1 <= c2:
            for i in xrange(c1, c2+1):
                res[r1][i] = num
                num += 1
            r1 += 1
            if r1 > r2 or c1 > c2:
                break
            for i in xrange(r1, r2+1):
                res[i][c2] = num
                num += 1
            c2 -= 1
            if r1 > r2 or c1 > c2:
                break
            for i in xrange(c2, c1-1, -1):
                res[r2][i] = num
                num += 1
            r2 -= 1
            if r1 > r2 or c1 > c2:
                break
            for i in xrange(r2, r1-1, -1):
                res[i][c1] = num
                num += 1
            c1 += 1
            if r1 > r2 or c1 > c2:
                break
        return res
</pre>
