---
layout: post
title: LeetCode | Palindrome Partitioning in Python
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
    Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.

Algorithm:
    DFS
    fist get the valid palindrome table for more efficient queries
'''


class Solution:
    # @param s, a string
    # @return a list of lists of string
    def partition(self, s):
        table = [[True if itr2 == itr else False for itr2 in xrange(len(s))] for itr in xrange(len(s))]
        for i in xrange(len(s) - 2, -1, -1):
            for j in xrange(i+1, len(s)):
                if s[i] == s[j]:
                    table[i][j] = table[i+1][j-1] if i+1 <= j-1 else True
        res = []
        self.partition_rec(s, 0, res, [], table)
        return res

    def partition_rec(self, s, start, res, tmp, table):
        if start == len(s):
            res.append(tmp[:])
        for i in xrange(start, len(s)):
            if table[start][i]:
                tmp.append(s[start:i+1])
                self.partition_rec(s, i+1, res, tmp, table)
                tmp.pop()
</pre>
