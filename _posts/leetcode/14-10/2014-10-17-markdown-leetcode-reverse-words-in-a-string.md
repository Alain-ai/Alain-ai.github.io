---
layout: post
title: LeetCode | Reverse Words in a String in Python
categories: LeetCode
tags: Python

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
jax: ["input/TeX","output/HTML-CSS"],
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]},
extensions: ["tex2jax.js","MathMenu.js","MathZoom.js"],
TeX: { equationNumbers: { autoNumber: "AMS" }, extensions: ["AMSmath.js", "AMSsymbols.js","noErrors.js","noUndefined.js"]}
});
</script>

<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML">
</script>

<pre>
'''
Question:
    Given an input string, reverse the string word by word.

Algorithm:
    ...
'''


class Solution:
    # @param s, a string
    # @return a string
    def reverseWords(self, s):
        return ' '.join(re.compile('\s+').split(s.strip())[::-1])
</pre>
