---
layout: post
title: LeetCode | Valid Number in Python
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
    Validate if a given string is numeric.

Algorithm:
    re match
'''


class Solution:
    # @param s, a string
    # @return a boolean
    def isNumber(self, s):
        return True if re.compile('^[-+]?(\d+\.?\d*|\.\d+)([Ee][+-]?\d+)?$').match(s.strip()) else False
</pre>
