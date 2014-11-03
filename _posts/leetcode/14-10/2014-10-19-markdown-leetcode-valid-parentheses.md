---
layout: post
title: LeetCode | Valid Parentheses in Python
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
    Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid. The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

Algorithm:
    stack
'''


class Solution:
    # @return a boolean
    def isValid(self, s):
        stk = []
        for e in s:
            if e == '(' or e == '[' or e == '{':
                stk.append(e)
            else:
                if not stk:
                    return False
                if e == ')' and stk.pop() != '(':
                    return False
                if e == ']' and stk.pop() != '[':
                    return False
                if e == '}' and stk.pop() != '{':
                    return False
        return len(stk) == 0
</pre>
