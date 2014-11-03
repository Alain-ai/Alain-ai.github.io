---
layout: post
title: LeetCode | Multiply Strings  in Python
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
Question: Given two numbers represented as strings, return multiplication of the numbers as a string. The numbers can be arbitrarily large and are non-negative.

Algorithm: To get the ith number,
    1. iterate j and k from num1 and num2 such that i == j
    2. sum over all num1[j] * num2[k] based on possible combinations of j and k
    3. ith number is sum % 10, carry is sum / 10
'''


class Solution:
    # \@param num1, a string
    # \@param num2, a string
    # \@return a string
    def multiply(self, num1, num2):
        num1 = num1[::-1]
        num2 = num2[::-1]
        l1, l2 = len(num1), len(num2)
        carry = 0
        res = []
        for i in xrange(l1+l2-1):
            tmp = carry
            for j in xrange(l1):
                k = i - j
                if 0 <= k < l2:
                    tmp += int(num1[j]) * int(num2[k])
            res.append(str(tmp % 10))
            carry = tmp / 10
        if carry:
            res += list(str(carry)[::-1])
        while len(res) > 1 and res[-1] == '0':
            res.pop()
        return ''.join(res)[::-1]
</pre>
