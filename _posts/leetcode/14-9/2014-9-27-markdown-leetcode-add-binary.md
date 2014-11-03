---
layout: post
title: LeetCode | Add Binary in Python
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
    Given two binary strings, return their sum (also a binary string).

Algorithm:
    add one by one from the tail and be careful when the left carry is not 0
'''


class Solution:
    # @param a, a string
    # @param b, a string
    # @return a string
    def addBinary(self, a, b):
        a, b = a[::-1], b[::-1]
        i = j = carry = 0
        res = []
        while i < len(a) and j < len(b):
            tmp = int(a[i]) + int(b[j]) + carry
            carry = tmp / 2
            res.append(str(tmp % 2))
            i, j = i + 1, j + 1
        while i < len(a):
            tmp = int(a[i]) + carry
            carry = tmp / 2
            res.append(str(tmp % 2))
            i += 1
        while j < len(b):
            tmp = int(b[j]) + carry
            carry = tmp / 2
            res.append(str(tmp % 2))
            j += 1
        if carry:
            res.append(str(carry))
        while len(res) > 1 and res[-1] == '0':
            res.pop()
        return ''.join(res)[::-1]
</pre>
