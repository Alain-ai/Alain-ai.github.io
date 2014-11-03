---
layout: post
title: LeetCode | Generate Parentheses in Python
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
    Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

Algorithm:
    DFS
'''


class Solution:
    # @param an integer
    # @return a list of string
    def generateParenthesis(self, n):
        res = []
        self.generateParenthesis_rec(n, n, res, '')
        return res
        
    def generateParenthesis_rec(self, l, r, res, tmp):
        if r < l:
            return
        elif r == l == 0:
            res.append(tmp)
        else:
            if l:
                self.generateParenthesis_rec(l-1, r, res, tmp+'(')
            if r:
                self.generateParenthesis_rec(l, r-1, res, tmp+')')
</pre>
