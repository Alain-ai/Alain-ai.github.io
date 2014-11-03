---
layout: post
title: LeetCode | Next Permutation in Python
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
    Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers. If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order). The replacement must be in-place, do not allocate extra memory.



Algorithm:
    ...
'''


class Solution:
    # @param num, a list of integer
    # @return a list of integer
    def nextPermutation(self, num):
        for i in xrange(len(num) - 2, -1, -1):
            for j in xrange(len(num) - 1, i, -1):
                if num[i] < num[j]:
                    num[i], num[j] = num[j], num[i]
                    num[i+1:] = num[i+1:][::-1]
                    return num
        return num[::-1]
</pre>
