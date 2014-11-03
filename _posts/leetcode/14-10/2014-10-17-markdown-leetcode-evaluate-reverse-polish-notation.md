---
layout: post
title: LeetCode | Evaluate Reverse Polish Notation in Python
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
    Evaluate the value of an arithmetic expression in Reverse Polish Notation. Valid operators are +, -, *, /. Each operand may be an integer or another expression.

Algorithm:
    stack

Note:
    division of python is floor division
'''


class Solution:
    # @param tokens, a list of string
    # @return an integer
    def evalRPN(self, tokens):
        stk, ops = [], set(['+', '-', '*', '/'])
        for t in tokens:
            if t not in ops:
                stk.append(int(t))
            else:
                op2, op1 = stk.pop(), stk.pop()
                if t == '+':
                    stk.append(op1 + op2)
                elif t == '-':
                    stk.append(op1 - op2)
                elif t == '*':
                    stk.append(op1 * op2)
                elif t == '/':
                    stk.append(int(float(op1) / float(op2)))
        return stk[-1]
</pre>
