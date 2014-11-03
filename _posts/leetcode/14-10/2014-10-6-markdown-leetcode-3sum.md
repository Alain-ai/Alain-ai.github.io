---
layout: post
title: LeetCode | 3Sum in Python
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
    Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:
    1. Elements in a triplet (a,b,c) must be in non-descending order. (ie, a ≤ b ≤ c)
    2. The solution set must not contain duplicate triplets.

Algorithm:
    fix one and approach from two sides to the middle
'''


class Solution:
    # @return a list of lists of length 3, [[val1,val2,val3]]
    def threeSum(self, num):
        num.sort()
        res = []
        if len(num) < 3:
            return res
        for i in xrange(len(num)-2):
            if i > 0 and num[i-1] == num[i]:
                continue
            target = -num[i]
            j, k = i+1, len(num) - 1
            while j < k:
                if j > i+1 and num[j] == num[j-1]:
                    j += 1
                    continue
                if num[j] + num[k] > target:
                    k -= 1
                elif num[j] + num[k] < target:
                    j += 1
                else:
                    res.append([num[i], num[j], num[k]])
                    j, k = j + 1, k - 1
        return res
</pre>
