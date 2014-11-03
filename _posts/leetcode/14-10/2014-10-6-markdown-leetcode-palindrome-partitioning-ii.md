---
layout: post
title: LeetCode | Palindrome Partitioning II in Python
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
    Given a string s, partition s such that every substring of the partition is a palindrome. Return the minimum cuts needed for a palindrome partitioning of s.

Algorithm:
    DP
    fist get the valid palindrome table for more efficient queries
    DP[i] = min(DP[j]+1), 0 <= j <= i-1
'''


class Solution:
    # @param s, a string
    # @return an integer
    def minCut(self, s):
        if not s:
            return 0
        l = len(s)
        table = [[True if itr2 == itr else False for itr2 in xrange(l)] for itr in xrange(l)]
        for i in xrange(l-2, -1, -1):
            for j in xrange(i+1, l):
                if s[i] == s[j]:
                    table[i][j] = table[i+1][j-1] if i+1 <= j-1 else True
        DP = [0 for itr in xrange(l)]
        for i in xrange(1, l):
            DP[i] = DP[i-1] + 1
            for j in xrange(i+1):
                if table[j][i]:
                    DP[i] = min(DP[i], DP[j-1]+1 if j-1 >= 0 else 0)
        return DP[-1]
</pre>
