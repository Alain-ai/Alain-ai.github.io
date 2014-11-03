---
layout: post
title: LeetCode | Longest Valid Parentheses in Python
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
    Given a string containing just the characters "(" and ")", find the length of the longest valid (well-formed) parentheses substring. For "(()", the longest valid parentheses substring is "()", which has length = 2. Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.

Algorithm:
    one dimension DP
    "rec" stores the length of the longest valid parentheses substring which ends up at index i
'''


class Solution:
    # @param s, a string
    # @return an integer
    def longestValidParentheses(self, s):
        # corner case: len(s) <= 1, not valid parenthesis pair
        if len(s) <= 1:
            return 0
        rec = [0 for itr in xrange(len(s))]
        for i in xrange(len(s)):
            if s[i] == ')' and i > 0:
                j = i - 1 - rec[i - 1]
                if j >= 0 and s[j] == '(':
                    rec[i] = 2 + rec[i-1]
                    if j > 0:
                        rec[i] += rec[j-1]
        print rec
        return max(rec)
</pre>
