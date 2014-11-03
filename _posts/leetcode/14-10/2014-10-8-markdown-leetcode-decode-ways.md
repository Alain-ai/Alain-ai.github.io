---
layout: post
title: LeetCode | Decode Ways in Python
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
    A message containing letters from A-Z is being encoded to numbers using the following mapping:

    "A" -> 1
    "B" -> 2
    ...
    "Z" -> 26
    Given an encoded message containing digits, determine the total number of ways to decode it.

Algorithm:
    DP, a variant of Fibo
    DP[i] = DP[i] + DP[i-1] if 1 <= s[i] <= 9
    DP[i] = DP[i] + DP[i-2]  if 10 <= s[i-1:i+1] <= 26
'''


class Solution:
    # @param s, a string
    # @return an integer
    def numDecodings(self, s):
        if len(s) == 0:
            return 0
        check = set([str(itr) for itr in xrange(10, 27)])
        DP = [1 if 1 <= int(s[0]) <= 9 else 0] + [0 for itr in xrange(len(s)-1)]
        for i in xrange(1, len(s)):
            DP[i] = DP[i-1] if 1 <= int(s[i]) <= 9 else 0
            if s[i-1:i+1] in check:
                DP[i] += DP[i-2] if i >= 2 else 1
        return DP[-1]
</pre>
