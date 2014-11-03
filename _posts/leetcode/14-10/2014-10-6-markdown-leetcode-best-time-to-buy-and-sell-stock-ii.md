---
layout: post
title: LeetCode | Best Time to Buy and Sell Stock II in Python
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
    Say you have an array for which the ith element is the price of a given stock on day i. Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

Algorithm:
    Greedy
    earn as much as possible between every two days
'''


class Solution:
    # @param prices, a list of integer
    # @return an integer
    def maxProfit(self, prices):
        if not prices or len(prices) == 1:
            return 0
        res = 0
        for i in xrange(1, len(prices)):
            res += prices[i] - prices[i-1] if prices[i] - prices[i-1] > 0 else 0
        return res
</pre>
