---
layout: post
title: LeetCode | Restore IP Addresses in Python
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
    Given a string containing only digits, restore it by returning all possible valid IP address combinations.

Algorithm:
    DFS

Note:
    not leading zeros for non-zero numbers
'''


class Solution:
    # @param s, a string
    # @return a list of strings
    def restoreIpAddresses(self, s):
        res = []
        self.restoreIpAddresses_rec(0, s, res, [])
        return res

    def restoreIpAddresses_rec(self, level, s, res, stk):
        if level == 4 and s == '':
            res.append('.'.join(stk))
            return
        if level >= 5 or s == '':
            return
        for i in xrange(min(3, len(s))):
            pre = s[:i+1]
            if pre == '0'or (not pre.startswith('0') and 1 <= int(pre) <= 255):
                stk.append(pre)
                self.restoreIpAddresses_rec(level + 1, s[i+1:], res, stk)
                stk.pop()
</pre>
