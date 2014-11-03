---
layout: post
title: LeetCode | Longest Palindromic Substring in Python
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
    Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

Algorithm:
    1. extend i to two ends
    2. extend i and i+1 to two ends
'''


class Solution:
    # @return a string
    def longestPalindrome(self, s):
        max_s = ''
        for i in xrange(len(s)):
            s1 = self.extend(s, i)
            if len(s1) > len(max_s):
                max_s = s1
            s2 = self.extend(s, i, i+1)
            if len(s2) > len(max_s):
                max_s = s2
        return max_s

    def extend(self, s, i, j=None):
        if j:
            while i >= 0 and j < len(s) and s[i] == s[j]:
                i, j = i - 1, j + 1
            return s[i+1:j]
        else:
            j, k = i - 1, i + 1
            while j >= 0 and k < len(s) and s[j] == s[k]:
                j, k = j - 1, k + 1
            return s[j+1:k]
</pre>
