---
layout: post
title: LeetCode | Populating Next Right Pointers in Each Node in Python
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
    Given a binary tree

    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }

    Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL. Initially, all next pointers are set to NULL.

    Note: You may only use constant extra space. You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children). For example, Given the following perfect binary tree,

         1
       /  \
      2    3
     / \  / \
    4  5  6  7

    After calling your function, the tree should look like:

         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL

Algorithm:
    BFS
    link the head of queue with its successor
'''


class Solution:
    # @param root, a tree node
    # @return nothing
    def connect(self, root):
        if not root:
            return None
        q = collections.deque([root, None])
        while q:
            node = q.popleft()
            if not node:
                if not q:
                    break
                q.append(None)
            else:
                node.next = q[0]
                if node.left:
                    q.append(root.left)
                if node.right:
                    q.append(root.right)
</pre>
