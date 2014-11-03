---
layout: post
title: LeetCode | Largest Rectangle in Histogram in Python
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
    Given n non-negative integers representing the histogram\'s bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

Algorithm:
    1. For every possible rectangle we can get, we define the supporter of it as the lowest bar(with the smallest value).
    2. For every bar, we extend the rectangle as much as possbile that is supported by the bar.
    3. Using stack we are able to reduce the time to compute such a rectangle to O(1)
    4. For n bars entirely, we can solve the problem in O(n) time.
'''


class Solution:
    # @param height, a list of integer
    # @return an integer
    def largestRectangleArea(self, height):
        height = [0] + height + [0]
        res, stk = 0, [0]
        for i in xrange(1, len(height)):
            if height[i] >= height[stk[-1]]:
                stk.append(i)
            else:
                while height[i] < height[stk[-1]]:
                    idx = stk.pop()
                    res = max(res, (i - stk[-1] - 1) * height[idx])
                stk.append(i)
        return res
</pre>
