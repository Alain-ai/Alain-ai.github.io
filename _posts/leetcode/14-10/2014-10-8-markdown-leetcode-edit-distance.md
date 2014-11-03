---
layout: post
title: LeetCode | Edit Distance in Python
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
    Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.) You have the following 3 operations permitted on a word:
    a) Insert a character
    b) Delete a character
    c) Replace a character

Algorithm:
    DP
    DP[i][j] = min(DP[i-1][j]+1, DP[i][j-1]+1, (DP[i-1][j-1] + (0 if word1[i-1] == word2[j-1] else 1)))
'''


class Solution:
    # @return an integer
    def minDistance(self, word1, word2):
        l1, l2 = len(word1), len(word2)
        DP = [[0 for itr in xrange(l2+1)] for itr2 in xrange(l1+1)]
        for i in xrange(1, l2+1):
            DP[0][i] = DP[0][i-1] + 1
        for i in xrange(1, l1+1):
            DP[i][0] = DP[i-1][0] + 1
        for i in xrange(1, l1+1):
            for j in xrange(1, l2+1):
                DP[i][j] = min(DP[i-1][j]+1, DP[i][j-1]+1, (DP[i-1][j-1] + (0 if word1[i-1] == word2[j-1] else 1)))
        return DP[l1][l2]
</pre>
