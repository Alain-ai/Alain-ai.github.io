---
layout: post
title: LeetCode | Maximum Product Subarray in Python
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
    Find the contiguous subarray within an array (containing at least one number) which has the largest product.

Algorithm:
    two tables(DP_max, DP_min) to store the max and min at currenet index i by compareing three values(A[i], A[i] * DP_max[-1], A[i] * DP_min[-1]) respectively
'''


class Solution:
    # @param A, a list of integers
    # @return an integer
    def maxProduct(self, A):
        ps, ns = [A[0]], [A[0]]
        for i in xrange(1, len(A)):
            tp, tn = ps[-1], ns[-1]
            ps.append(max(A[i], A[i] * tp, A[i] * tn))
            ns.append(min(A[i], A[i] * tn, A[i] * tp))
        return max(ps)
</pre>
