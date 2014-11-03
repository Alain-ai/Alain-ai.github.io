---
layout: post
title: LeetCode | ZigZag Conversion in Python
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
    The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

    P   A   H   N
    A P L S I I G
    Y   I   R
    And then read line by line: "PAHNAPLSIIGYIR"

Algorithm:
    follow the zig-zag manner
'''


class Solution:
    # @return a string
    def convert(self, s, nRows):
        if nRows == 1:
            return s
        nCol = (nRows - 1) * ((len(s) / (2 * nRows - 2)) + 1)
        mat = [[None for j in xrange(nCol)] for i in xrange(nRows)]
        r, c, idx = 0, 0, 0
        for unit in xrange(((len(s) / (2 * nRows - 2)) + 1)):
            for i in xrange(nRows - 1):
                if idx >= len(s):
                    return ''.join(mat[i][j] if mat[i][j] else '' for i in xrange(nRows) for j in xrange(nCol))
                mat[r][c] = s[idx]
                r, idx = r + 1, idx + 1
            for i in xrange(nRows - 1):
                if idx >= len(s):
                    return ''.join(mat[i][j] if mat[i][j] else '' for i in xrange(nRows) for j in xrange(nCol))
                mat[r][c] = s[idx]
                r, c, idx = r - 1, c + 1, idx + 1
        return ''.join(mat[i][j] if mat[i][j] else '' for i in xrange(nRows) for j in xrange(nCol))
</pre>
