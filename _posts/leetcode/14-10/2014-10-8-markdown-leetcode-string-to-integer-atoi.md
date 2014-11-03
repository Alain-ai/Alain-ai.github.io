---
layout: post
title: LeetCode | String to Integer (atoi) in Python
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
    There are two sorted arrays A and B of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

Algorithm:
    be careful about input cases

Note:
    1. starting with minus or plus sign
    2. starting with 0
    3. contain non-digit char
        1. beginning or middle
        2. end
        3. white space anywhere
    4. overflow?
'''


class Solution:
    # @return an integer
    def atoi(self, s):
        s = s.strip()
        if len(s) == 0:
            return 0
        minus = False
        if s[0] == '+':
            s = s[1:]
        elif s[0] == '-':
            s = s[1:]
            minus = True
        num = 0
        s = list(s)
        for i in xrange(len(s)):
            if not ('0' <= s[-1] <= '9'):
                s.pop()
            else:
                break
        s = ''.join(s)
        for i in xrange(len(s)):
            if ord('0') <= ord(s[i]) <= ord('9'):
                num = num * 10 + (ord(s[i]) - ord('0'))
            else:
                break
        if minus:
            if num > 2**31:
                return -(2**31)
            else:
                return -num
        else:
            if num > 2**31 - 1:
                return 2 ** 31 - 1
            else:
                return num
</pre>
