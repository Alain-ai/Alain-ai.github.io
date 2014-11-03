---
layout: post
title: LeetCode | Letter Combinations of a Phone Number in Python
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
    Given a digit string, return all possible letter combinations that the number could represent.

Algorithm:
    DFS
'''


class Solution:
    # @return a list of strings, [s1, s2]
    def letterCombinations(self, digits):
        if len(digits) == 0:
            return ['']
        mapper = [' ', '', 'abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz']
        digits = list(digits)
        res = self.letterCombinations_rec(mapper, digits)
        return map(lambda x: ''.join(x), res)

    def letterCombinations_rec(self, mapper, digits):  # when it won't construct a valid element in the very last recursion, just return something in every step and construct based on what has been returned
        res = []
        if len(digits) == 1:
            for s in mapper[int(digits[0])]:
                res.append([s])
        else:
            tmp = self.letterCombinations_rec(mapper, digits[1:])
            for r in tmp:
                for s in mapper[int(digits[0])]:
                    res.append([s] + r)
        return res
</pre>
