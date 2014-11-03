---
layout: post
title: LeetCode | Merge Intervals in Python
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
    Given a collection of intervals, merge all overlapping intervals.

Algorithm:
    1. sort intervals based on start first and on end second
    2. intervals[i].start > cur_end, stop current merging
    3. intervals[i].start <= cur_end, greedily find the maximum possible end of intervals[i].end and cur_end

Note:
    multiple ways of sorting have been performed
    x.sort() is identical to sorted(x), they have the same set of parameters
    "cmp" takes two argument and returns an integr
    "key" takes one argument and returns the value we want to use in this sort
'''


# Definition for an interval.
class Interval:
    def __init__(self, s=0, e=0):
        self.start = s
        self.end = e

    def __repr__(self):
        return '[' + str(self.start) + ' ' + str(self.end) + ']'

    # def __str__(self):
    #     return '[' + str(self.start) + ' ' + str(self.end) + ']'


import operator


class Solution:
    # @param intervals, a list of Interval
    # @return a list of Interval
    def merge(self, intervals):
        res = []
        if len(intervals) == 0:
            return res

        # def comparator(x, y):
        #     if isinstance(x, Interval) and isinstance(x, Interval):
        #         if x.start < y.start:
        #             return -1
        #         elif x.start == y.start:
        #             return x.end - y.end
        #         else:
        #             return 1
        #     else:
        #         raise

        # intervals.sort(cmp=comparator)
        # intervals.sort(key=operator.attrgetter('start') and operator.attrgetter('end'))
        intervals.sort(key=lambda x: (x.start, x.end))
        # intervals = sorted(intervals, key=operator.attrgetter('start') and operator.attrgetter('end'))
        # intervals = sorted(intervals, key=lambda x: (x.start, x.end))
        # intervals = sorted(intervals, cmp=comparator)

        cur_start, cur_end = intervals[0].start, intervals[0].end
        res = []
        for i in xrange(1, len(intervals)):
            start_i, end_i = intervals[i].start, intervals[i].end
            if start_i <= cur_end:
                cur_end = max(cur_end, end_i)
            else:
                res.append(Interval(cur_start, cur_end))
                cur_start = start_i
                cur_end = end_i
        res.append(Interval(cur_start, cur_end))
        return res
</pre>
