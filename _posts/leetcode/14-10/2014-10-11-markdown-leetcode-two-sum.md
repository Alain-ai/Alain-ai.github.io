---
layout: post
title: LeetCode | Two Sum in Python
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
    Given an array of integers, find two numbers such that they add up to a specific target number. The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based. You may assume that each input would have exactly one solution.

Algorithm:
    use a map to store what is expected
'''


class Solution:
    # @return a tuple, (index1, index2)
    def twoSum(self, num, target):
        i = 0
        cMap = {}
        while i < len(num):
            if target - num[i] in cMap.keys():
                return (cMap[target-num[i]] + 1, i + 1)
            else:
                cMap[num[i]] = i
            i += 1
        return (0, 0)
</pre>
