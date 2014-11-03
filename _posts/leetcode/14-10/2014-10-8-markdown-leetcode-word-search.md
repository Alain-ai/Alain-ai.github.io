---
layout: post
title: LeetCode | Word Search in Python
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
    Given a 2D board and a word, find if the word exists in the grid. The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

Algorithm:
    BFS
'''


class Solution:
    # @param board, a list of lists of 1 length string
    # @param word, a string
    # @return a boolean
    def exist(self, board, word):
        if len(board) == 0:
            return len(word) == 0
        m, n = len(board), len(board[0])
        visited = [[False for itr in xrange(n)] for itr2 in xrange(m)]
        for i in xrange(m):
            for j in xrange(n):
                if self.exist_rec(board, word, 0, i, j, visited):
                    return True
        return False

    def exist_rec(self, board, word, level, row, col, visited):
        if level == len(word):
            return True
        else:
            m, n = len(board), len(board[0])
            if 0 <= row <= m and 0 <= col <= n and board[row][col] == word[level] and not visited[row][col]:
                visited[row][col] = True
                if self.exist_rec(board, word, level+1, row-1, col, visited):
                    return True
                if self.exist_rec(board, word, level+1, row+1, col, visited):
                    return True
                if self.exist_rec(board, word, level+1, row, col-1, visited):
                    return True
                if self.exist_rec(board, word, level+1, row, col+1, visited):
                    return True
                visited[row][col] = False
            else:
                return False
</pre>
