---
layout: post
title: LeetCode | Recover Binary Search Tree in Python
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
    Two elements of a binary search tree (BST) are swapped by mistake. Recover the tree without changing its structure.

Algorithm:
    get two violations in two kinds of Inorder traversal(left goes first and right goes firsts)
'''


class Solution:
    # @param root, a tree node
    # @return a tree node

    def recoverTree(self, root):
        succ = []
        self.get_left_wrong(root, [], succ)
        l = succ[0]
        succ = []
        self.get_right_wrong(root, [], succ)
        r = succ[0]
        # print l, r
        l.val, r.val = r.val, l.val
        return root

    def get_left_wrong(self, root, box, succ):
        if succ:
            return succ
        if root.left:
            self.get_left_wrong(root.left, box, succ)
        box.append(root)
        if len(box) > 2:
            box.pop(0)
        if len(box) == 2 and box[0].val > box[1].val:
            succ.append(box[0])
        if root.right:
            self.get_left_wrong(root.right, box, succ)

    def get_right_wrong(self, root, box, succ):
        if succ:
            return succ
        if root.right:
            self.get_right_wrong(root.right, box, succ)
        box.append(root)
        if len(box) > 2:
            box.pop(0)
        if len(box) == 2 and box[0].val < box[1].val:
            succ.append(box[0])
        if root.left:
            self.get_right_wrong(root.left, box, succ)
</pre>
