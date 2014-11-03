---
layout: post
title: LeetCode | Substring with Concatenation of All Words in Python
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
    You are given a string, S, and a list of words, L, that are all of the same length. Find all starting indices of substring(s) in S that is a concatenation of each word in L exactly once and without any intervening characters.

Algorithm:
    ...

Note:
    can not get accepted sigh
'''


class Solution:
    # @param S, a string
    # @param L, a list of string
    # @return a list of integer
    def findSubstring(self, S, L):
        res = []
        if len(S) == 0 or len(L) == 0:
            return res
        len_S = len(S)
        len_L = len(L)
        len_T = len(L[0]) * len_L
        res = []
        req = dict()
        for itr in L:
            req[itr] = req.get(itr, 0) + 1
        for i in xrange(len_S - len_T):
            S1 = S[i:i+len_T]
            j = 0
            req_local = dict(req)
            while j < len_L:
                s = S1[j*len(L[0]):(j+1) * len(L[0])]
                if s not in req_local or req_local[s] <= 0:
                    break
                req_local[s] -= 1
                j += 1
            if j == len_L:
                res.append(i)
        return res
</pre>
