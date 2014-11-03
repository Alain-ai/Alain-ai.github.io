---
layout: post
title: LeetCode | Implement strStr() in Python
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
    Implement strStr(). Returns a pointer to the first occurrence of needle in haystack, or null if needle is not part of haystack.

Algorithm:
    1. Horspool algorithm
    2. Karp-Rabin algorithm
'''


class Solution:
    # @param haystack, a string
    # @param needle, a string
    # @return a string or None
    def strStr(self, haystack, needle):
        n, m, ab = len(haystack), len(needle), set(needle)
        mapper = dict(zip(ab, [m] * len(ab)))
        for i in xrange(m - 1):
            mapper[needle[i]] = m - 1 - i
        i = m - 1
        while i < n:
            j, k = m - 1, i
            while j >= 0:
                if needle[j] == haystack[k]:
                    j, k = j - 1, k - 1
                else:
                    if i == n - 1: return None
                    shift = mapper.get(haystack[i], m)
                    i = min(i + shift, n - 1)
                    break
            if j < 0:
                return needle + haystack[i+1:]
        return None


    def strStr(self, haystack, needle):
        n, m = len(haystack), len(needle)
        h_t, h_p = self.hashcode(haystack[:m]), self.hashcode(needle)
        for i in xrange(n-m+1):
            if h_t == h_p:
                if haystack[i:i+m] == needle:
                    return haystack[i:]
            else:
                if i+m < n:
                    h_t = (31 * (h_t - (31**(m-1)*ord(haystack[i]))) + ord(haystack[i+m])) % ((1<<31) - 1)

    def hashcode(self, s):
        h = 0
        for sub in s:
            h = (31 * h + ord(sub)) % ((1<<31) - 1)
        return h
</pre>


To learn more about KMP algorithm, watch these two videos.

* Principle
<iframe width="560" height="315" src="//www.youtube.com/embed/EEjNb9yUv1k" frameborder="0" allowfullscreen></iframe>
* PreProcessing
<iframe width="560" height="315" src="//www.youtube.com/embed/RYUGTzI-f-A" frameborder="0" allowfullscreen></iframe>
