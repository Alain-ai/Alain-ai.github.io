---
layout: post
title: LeetCode | Binary Tree Level Order Traversal in Python
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
    Given a binary tree, return the level order traversal of its nodes\' values. (ie, from left to right, level by level). For example: Given binary tree {3,9,20,#,#,15,7},

    3
   / \
  9  20
    /  \
   15   7
   return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]

Algorithm:
    BFS
'''


class Solution:
    # @param root, a tree node
    # @return a list of lists of integers
    def levelOrder(self, root):
        res = []
        if not root:
            return res
        q = deque([root, None])
        res = []
        tmp = []
        while q:
            node = q.popleft()
            if not node:
                res.append(tmp)
                tmp = []
                if not q:
                    break
                q.append(None)
            else:
                tmp.append(node.val)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
        return res
</pre>
