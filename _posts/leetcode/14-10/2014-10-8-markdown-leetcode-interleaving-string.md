---
layout: post
title: LeetCode | Interleaving String in Python
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
    Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

Algorithm:
    whether s1[0:i] and s2[0:j] interleave and form s3[0:i+j]
    DP[i][j] = DP[i-1][j] if s3[0:i+j-1] == s1[i-1]
    DP[i][j] = DP[i][j-1] if s3[0:i+j-1] == s2[j-1]
'''


class Solution:
    # @return a boolean
    def isInterleave(self, s1, s2, s3):
        if len(s3) != len(s1) + len(s2):
            return False
        DP = [[False for itr in xrange(len(s2)+1)] for itr2 in xrange(len(s1)+1)]
        DP[0][0] = True
        for i in xrange(1, len(s2)+1):
            DP[0][i] = False if s3[i-1] != s2[i-1] else DP[0][i-1]
        for i in xrange(1, len(s1)+1):
            DP[i][0] = False if s3[i-1] != s1[i-1] else DP[i-1][0]
        for i in xrange(1, len(s1)+1):
            for j in xrange(1, len(s2)+1):
                if s3[i-1+j-1+1] == s1[i-1]:
                    DP[i][j] = DP[i-1][j]
                if not DP[i][j] and s3[i-1+j-1+1] == s2[j-1]:
                    DP[i][j] = DP[i][j-1]
        return DP[len(s1)][len(s2)]
</pre>
