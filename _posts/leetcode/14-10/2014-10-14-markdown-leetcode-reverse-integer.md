---
layout: post
title: LeetCode | Reverse Integer in Python
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
    Reverse digits of an integer.

Algorithm:
    division and mod operations
'''


class Solution:
    # @return an integer
    def reverse(self, x):
        if x == 0:
            return 0
        is_neg = False
        if x < 0:
            is_neg = True
            x = abs(x)
        res = 0
        while x > 0:
            res = res * 10 + x % 10
            x /= 10
        return -res if is_neg else res
</pre>
