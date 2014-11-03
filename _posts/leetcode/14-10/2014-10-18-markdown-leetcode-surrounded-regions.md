---
layout: post
title: LeetCode | Surrounded Regions in Python
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
    Given a 2D board containing 'X' and 'O', capture all regions surrounded by 'X'. A region is captured by flipping all 'O's into 'X's in that surrounded region.

Algorithm:
    BFS

Note:
    1. do not need visited table
    2. do not use a function to implement the statement "0 <= n_x < len(board) and 0 <= n_y < len(board[0]) and board[n_x][n_y] == 'O'"
'''


class Solution:
    # @param board, a 2D array
    # Capture all regions by modifying the input board in-place.
    # Do not return any value.
    def solve(self, board):
        for i in xrange(len(board)):
            for j in xrange(len(board[0])):
                if (i == 0 or j == 0 or i == len(board)-1 or j == len(board[0])-1) and board[i][j] == 'O':
                    self.solve_rec(board, i, j)
        for i in xrange(len(board)):
            for j in xrange(len(board[0])):
                board[i][j] = 'O' if board[i][j] == '?' else 'X'

    def solve_rec(self, board, i, j):
        q = collections.deque([(i, j)])
        while q:
            x, y = q.popleft()
            board[x][y] = '?'
            n_x, n_y = x + 1, y
            if 0 <= n_x < len(board) and 0 <= n_y < len(board[0]) and board[n_x][n_y] == 'O':
                board[n_x][n_y] = '?'
                q.append((n_x, n_y))
            n_x, n_y = x - 1, y
            if 0 <= n_x < len(board) and 0 <= n_y < len(board[0]) and board[n_x][n_y] == 'O':
                board[n_x][n_y] = '?'
                q.append((n_x, n_y))
            n_x, n_y = x, y + 1
            if 0 <= n_x < len(board) and 0 <= n_y < len(board[0]) and board[n_x][n_y] == 'O':
                board[n_x][n_y] = '?'
                q.append((n_x, n_y))
            n_x, n_y = x, y - 1
            if 0 <= n_x < len(board) and 0 <= n_y < len(board[0]) and board[n_x][n_y] == 'O':
                board[n_x][n_y] = '?'
                q.append((n_x, n_y))</pre>
