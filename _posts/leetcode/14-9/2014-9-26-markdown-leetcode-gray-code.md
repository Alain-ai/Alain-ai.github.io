---
layout: post
title: LeetCode | Gray Code in Python
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
    The gray code is a binary numeral system where two successive values differ in only one bit. Given a non-negative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.

Algorithm:
    DFS
    when we get the result for n-1 denoted as "sub", we can get that for n as "res" in the following way:
    1. "res" = "sub"
    2. reverse "sub"
    3. put 1 at the beginning of each element of the reversed "sub" and get "temp"
    4. "res" += "temp"
'''


class Solution:
    # @return a list of integers
    def grayCode(self, n):
        if n == 0:
            return [0]
        else:
            sub = self.grayCode(n-1)
            return sub + [(sub[i] | (1 << (n-1))) for i in xrange(len(sub)-1, -1, -1)]
</pre>
