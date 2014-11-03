---
layout: post
title: LeetCode | Regular Expression Matching in Python
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
    Implement regular expression matching with support for '.' and '*'. '.' Matches any single character. '*' Matches zero or more of the preceding element. The matching should cover the entire input string (not partial).

Algorithm:
    single char match: s<--1 and p<--1
    multiple char match: (s<--1 and p<--0) or (s<--0 and p<--2)
'''


class Solution:
    # @return a boolean
    def isMatch(self, s, p):
        if not p:
            return s == ''
        if s and (p[-1] == '.' or p[-1] == s[-1]):
            return self.isMatch(s[:-1], p[:-1])
        elif p[-1] == '*':
            if p[-2] == '.' or (s and p[-2] == s[-1]):
                return self.isMatch(s, p[:-2]) or (len(s) > 0 and self.isMatch(s[:-1], p))
            else:
                return self.isMatch(s, p[:-2])
        else:
            return False
</pre>
