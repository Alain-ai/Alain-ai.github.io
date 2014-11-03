---
layout: post
title: LeetCode | Divide Two Integers in Python
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
    Divide two integers without using multiplication, division and mod operator.

Algorithm:
    1. obtain divisor times power of 2 list
    2. accumulate the result by substracting the element of the list from the original dividend
'''


class Solution:
    # @return an integer
    def divide(self, dividend, divisor):
        # corner cases: minus, dividend < divisor, divisor = +(-)1, dividend == 0
        # more corner case: divisor == -(2**31)
        if dividend == 0:
            return 0
        if divisor == 1:
            return dividend
        if divisor == -1:
            return -dividend
        if divisor == -(2**31):
            return 0 if dividend != divisor else 1
        if (dividend > 0 and divisor > 0) or (dividend < 0 and divisor < 0):
            return self.apply_divide(abs(dividend), abs(divisor))
        else:
            return -self.apply_divide(abs(dividend), abs(divisor))

    def apply_divide(self, dividend, divisor):
        d = divisor
        d_list = []
        MAX = 2**31 - 1
        while d <= MAX and d <= dividend:
            d_list.append(d)
            d *= 2
        dvd = dividend
        idx = len(d_list) - 1
        res = 0
        while dvd >= divisor:
            if dvd >= d_list[idx]:
                dvd -= d_list[idx]
                res += 2 ** idx
            else:
                idx -= 1
        return res
</pre>
