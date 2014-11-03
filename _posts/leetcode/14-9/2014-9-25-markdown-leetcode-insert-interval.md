---
layout: post
title: LeetCode | Insert Interval in Python
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
    Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary). You may assume that the intervals were initially sorted according to their start times.

Algorithm:
    potential merging
        starts when intervals[i].end >= newInterval.start
        ends when intervals[i].start > new_end, where new_end means the max end in current merging result
    during merging
        always find the earliest start and latest end in a greedy way
'''


class Interval:
    def __init__(self, s=0, e=0):
        self.start = s
        self.end = e


class Solution:
    # @param intervals, a list of Intervals
    # @param newInterval, a Interval
    # @return a list of Interval
    def insert(self, intervals, newInterval):
        res = []
        if len(intervals) == 0:
            return res + [newInterval]
        i = 0
        while i < len(intervals):
            if intervals[i].end < newInterval.start:
                res.append(intervals[i])
                i += 1
            else:
                break
        new_start = newInterval.start
        new_end = newInterval.end
        while i < len(intervals):
            if intervals[i].start > new_end:
                break
            else:
                new_start = min(intervals[i].start, new_start)
                new_end = max(intervals[i].end, new_end)
            i += 1
        res.append(Interval(new_start, new_end))
        while i < len(intervals):
            res.append(intervals[i])
            i += 1
        return res
</pre>
