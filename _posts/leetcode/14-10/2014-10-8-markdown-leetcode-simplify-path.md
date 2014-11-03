---
layout: post
title: LeetCode | Simplify Path in Python
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
    Given an absolute path for a file (Unix-style), simplify it.

Algorithm:
    split + stack
'''


class Solution:
    # @param path, a string
    # @return a string
    def simplifyPath(self, path):
        metas = path.strip().split('/')
        stk = []
        for meta in metas:
            if not meta or meta == '.':
                continue
            elif meta == '..':
                if stk:
                    stk.pop()
            else:
                stk.append(meta)
        if not stk:
            return '/'
        res = ''
        for s in stk:
            res += '/' + s
        return res
</pre>
