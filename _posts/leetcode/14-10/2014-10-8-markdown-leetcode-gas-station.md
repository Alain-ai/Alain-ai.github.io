---
layout: post
title: LeetCode | Gas Station in Python
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
    There are N gas stations along a circular route, where the amount of gas at station i is gas[i]. You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations. Return the starting gas station\'s index if you can travel around the circuit once, otherwise return -1.

Note:
    The solution is guaranteed to be unique.

Algorithm:
    1. first get the left array
    2. start from some place where left > 0 denoted as i
    3. continue driving until "left_local" < 0 denoted as j
    4. start from j again because anywhere from i to j won\'t be better than i
'''


class Solution:
    # @param gas, a list of integers
    # @param cost, a list of integers
    # @return an integer
    def canCompleteCircuit(self, gas, cost):
        left = map(lambda x, y: x - y, gas, cost)
        i = 0
        if len(gas) == 1:
            return 0 if left[0] >= 0 else -1
        while i < len(gas):
            if left[i] <= 0:
                i += 1
                continue
            j, left_local = 1, left[i]
            while j < len(gas):
                k = (i + j) % len(gas)
                left_local += left[k]
                if left_local < 0:
                    i = i + j
                    break
                j += 1
            if j == len(gas):
                return i
            else:
                i += 1
        return -1
</pre>
