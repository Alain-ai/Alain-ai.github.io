---
layout: post
title: LeetCode | Distinct Subsequences in Python
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
    Given a string S and a string T, count the number of distinct subsequences of T in S. A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not). Here is an example: S = "rabbbit", T = "rabbit". Return 3.

Algorithm:
    DP
    DP[i][j] = DP[i][j-1] + DP[i-1][j-1], if T[i] == S[j]; because both T[0:i-1] <--> S[0:i-1] and T[0:i] <--> S[0:i-1] can contribute
    DP[i][j] = DP[i][j-1], otherwise; because only T[0:i] <--> S[0:i-1] contributes
'''


class Solution:
    # @return an integer
    def numDistinct(self, S, T):
        ls, lt = len(S), len(T)
        DP = [[0 for itr2 in xrange(ls)] for itr in xrange(lt)]
        DP[0] = [1 for itr in xrange(ls)]
        for i in xrange(1, lt+1):
            for j in xrange(i, ls+1):
                if T[i] == S[j]:
                    DP[i][j] = DP[i][j-1] + DP[i-1][j-1]
                else:
                    DP[i][j] = DP[i][j-1]
        return DP[lt][ls]
</pre>
