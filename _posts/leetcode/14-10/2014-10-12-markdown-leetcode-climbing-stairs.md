---
layout: post
title: LeetCode | Climbing Stairs in Python
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
    You are climbing a stair case. It takes n steps to reach to the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Algorithm:
    DP
'''


class Solution:
    # @param n, an integer
    # @return an integer
    def climbStairs(self, n):
        if n <= 0:
            return 0
        DP = [1, 2]
        if n <= 2:
            return DP[n-1]
        for i in xrange(2, n):
            DP.append(DP[i-1] + DP[i-2])
        return DP[-1]
</pre>
