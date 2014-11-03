---
layout: post
title: LeetCode | Single Number in Python
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
    Given an array of integers, every element appears twice except for one. Find that single one.

Algorithm:
    xor trick
'''


class Solution:
    # @param A, a list of integer
    # @return an integer
    def singleNumber(self, A):
        return reduce(lambda x, y: x^y, A)
</pre>
