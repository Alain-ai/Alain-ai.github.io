---
layout: post
title: LeetCode | Sqrt(x) in Python
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
    Implement int sqrt(int x). Compute and return the square root of x.

Algorithm:
    1. Newton\'s method
        1. f(t) = t^2 - x and t* is the solution
        2. first moment taylor expansion of f(t*) at current t
        3. f(t*) = f(t - h)
        4. x = f(t*) = f(t - h) = f(t) + f\'(t)(t-h-t) = f(t) - f\'(t)*h
        5. h = (f(t) - x) / f\'(t)
        6. h = (t^2 - x) / 2t
        7. given at current guess t, we are able to get the best step h
        8. then we take t - h as a better guess of t*
    2. binary search
        from 0 to x/2 + 1
'''


class Solution:
    # @param x, an integer
    # @return an integer
    def sqrt(self, x):
        if x == 0:
            return 0
        tp, t = 0., 1.
        while str(t) != str(tp):
            tp, t = t, (t**2. + x) / (2. * t)
        return int(str(t)[:str(t).index('.')])

    def sqrt1(self, x):
        i, j = 0, x/2 + 1
        while i <= j:
            mid = (i+j) >> 1
            s = mid * mid
            if s == x:
                return mid
            elif s > x:
                j = mid - 1
            else:
                i = mid + 1
        return j
</pre>
