---
layout: post
title: Find Path at Binary Tree
categories: algorithm
tags: Python

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>

Given a target node, we would like to find a path to it.

<pre>
def find_path(root, target, res):
    if not root:
        return False
    if root == target:
        res.append(root)
        return True
    res.append(root)
    found = find_path(root.left, target, res)
    if not found:
        found = find_path(root.right, target, res)
    if not found:
        res.pop()
        return False
    return True

def find_path(root, target, res, path):
    if not root:
        return
    if root == target:
        res.append(path + [target])
    path.append(root)
    find_path(root.left, target, res, path)
    find_path(root.right, target, res, path)
    path.pop()
</pre>
