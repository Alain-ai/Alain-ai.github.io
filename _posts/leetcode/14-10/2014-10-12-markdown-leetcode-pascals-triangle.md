---
layout: post
title: LeetCode | Binary Tree Maximum Path Sum in Python
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
    Given numRows, generate the first numRows of Pascal\'s triangle.

Algorithm:
    a number is equal to the sum of the two number on its shoulder if there exist
'''


class Solution:
    # @return a list of lists of integers
    def generate(self, numRows):
        if numRows == 0:
            return []
        if numRows == 1:
            return [1]
        res = [1]
        for i in xrange(1, numRows):
            sub = [1]
            for j in xrange(1, i):
                sub.append(res[i-1][j-1] + res[i-1][j])
            sub += [1]
            res.append(sub)
        return res
</pre>
