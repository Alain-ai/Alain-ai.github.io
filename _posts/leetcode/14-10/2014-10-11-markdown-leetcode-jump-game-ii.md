---
layout: post
title: LeetCode | Jump Game II in Python
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
    Implement pow(x, n).

Algorithm:
    Recursion
    1. n < 0
    2. n == 0
    3. n is odd
    4. n is even
'''


class Solution:
    # @param x, a float
    # @param n, a integer
    # @return a float
    def pow(self, x, n):
        if n == 0:
            return 1.
        if n < 0:
            return 1. / self.pow(x, -n)
        y = self.pow(x, n/2)
        if n & 1:
            return y * y * x
        else:
            return y * y
</pre>
