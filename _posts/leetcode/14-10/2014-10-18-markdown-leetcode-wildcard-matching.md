---
layout: post
title: LeetCode | Wildcard Matching in Python
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
    Implement wildcard pattern matching with support for '?' and '*'. '?' Matches any single character. '*' Matches any sequence of characters (including the empty sequence). The matching should cover the entire input string (not partial).

Algorithm:
    single char match: s-->1 and p-->1
    multiple char match: (s-->1 and p-->0) or (s-->0 and p-->2)

Note:
    Recursive version won\'t be accepted.
'''


class Solution:
    # @param s, an input string
    # @param p, a pattern string
    # @return a boolean
    def isMatch(self, s, p):
        p = re.sub('\*+', '*', p)
        return self.isMatch_itr(s, 0, p, 0)

    def isMatch_rec(self, s, i, p, j):
        if j == len(p):
            return i == len(s)
        if i < len(s):
            if s[i] == p[j] or p[j] == '?':
                return self.isMatch_rec(s, i+1, p, j+1)
            elif p[j] == '*':
                return self.isMatch_rec(s, i, p, j+1) or self.isMatch_rec(s, i+1, p, j)
            else:
                return False
        else:
            return j == len(p) - 1 and p[j] == '*'

    def isMatch_itr(self, s, i, p, j):
        stk = []
        while i < len(s):
            if j < len(p) and (s[i] == p[j] or p[j] == '?'):
                i, j = i + 1, j + 1
            elif j < len(p) and p[j] == '*':
                stk.append((i, j))
                j += 1
            else:
                if not stk:
                    return False
                else:
                    i, j = stk.pop()
                    i += 1
        return i == len(s) and (j == len(p) or (j == len(p) - 1 and p[-1] == '*'))
</pre>
