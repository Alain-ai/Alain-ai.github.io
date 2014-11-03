---
layout: post
title: LeetCode | Plus One in Python
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
    Given a non-negative number represented as an array of digits, plus one to the number. The digits are stored such that the most significant digit is at the head of the list.

Algorithm:
    straightforward
'''


class Solution:
    # @param digits, a list of integer digits
    # @return a list of integer digits
    def plusOne(self, digits):
        carry = 1
        i = len(digits) - 1
        while carry and i >= 0:
            d = digits[i] + carry
            carry = d / 10
            digits[i] = d % 10
            i -= 1
        if carry:
            return [1] + digits
        else:
            return digits
</pre>
