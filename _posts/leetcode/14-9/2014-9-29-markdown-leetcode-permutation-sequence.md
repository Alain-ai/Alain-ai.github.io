---
layout: post
title: LeetCode | Permutation Sequence in Python
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
    The set [1,2,3,…,n] contains a total of n! unique permutations. By listing and labeling all of the permutations in order. We get the following sequence (ie, for n = 3):
    1. "123"
    2. "132"
    3. "213"
    4. "231"
    5. "312"
    6. "321"
Given n and k, return the kth permutation sequence.

Algorithm:
    ...
'''


class Solution:
    # @return a string
    def getPermutation(self, n, k):
        fact = [1]
        for i in xrange(1, n-1):
            fact.append(fact[-1] * (i+1))
        repo = [i for i in xrange(1, n+1)]
        res, k = [], k - 1
        while k != 0:
            idx = k / fact[n-2]  # (n-1)!
            k = k % fact[n-2]
            res.append(repo.pop(idx))
            n -= 1
        return ''.join([str(i) for i in res + sorted(repo)])
</pre>
