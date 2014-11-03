---
layout: post
title: LeetCode | Anagrams in Python
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
    Given an array of strings, return all groups of strings that are anagrams.

Note:
    All inputs will be in lower-case.

Algorithm:
    1. sort by taking the sorted string as key
    2. group by the key
'''


class Solution:
    # @param strs, a list of strings
    # @return a list of strings
    def anagrams(self, strs):
        # sort based on sorted strings
        rec = []
        for s in strs:
            rec.append([''.join(sorted(s)), s])
        rec.sort()
        res = []
        for key, group in itertools.groupby(rec, operator.itemgetter(0)):
            tmp = map(lambda x: x[1], group)
            if len(tmp) > 1:
                res += tmp
        return res
</pre>
