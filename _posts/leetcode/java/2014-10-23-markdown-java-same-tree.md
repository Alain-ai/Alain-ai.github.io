---
layout: post
title: LeetCode | Same Tree in Java
categories: LeetCode
tags: Java

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>


<pre>
/*
    1. DFS 递归解法
    2. BFS 迭代解法
*/
public class Same_Tree{

    public boolean isSameTree(TreeNode p, TreeNode q) {
        return isSameTreeItr(p, q);
    }

    public boolean isSameTreeRec(TreeNode p, TreeNode q){
        if(p == null && q == null) return true;
        if(p == null || q == null) return false;
        if(p.val == q.val) return isSameTreeRec(p.left, q.left) && isSameTree(p.right, q.right);
        else return false;
    }

    public boolean isSameTreeItr(TreeNode p, TreeNode q){
        ArrayDeque<TreeNode> queue1 = new ArrayDeque<TreeNode>();
        ArrayDeque<TreeNode> queue2 = new ArrayDeque<TreeNode>();
        queue1.addLast(p);
        queue2.addLast(q);

        while(!queue1.isEmpty() && !queue2.isEmpty()){
            TreeNode n1 = queue1.removeFirst();
            TreeNode n2 = queue2.removeFirst();

            if(n1 == null && n2 == null) continue;
            if(n1 == null || n2 == null) return false;
            if(n1.val != n2.val) return false;

            queue1.addLast(n1.left);
            queue1.addLast(n1.right);
            queue2.addLast(n2.left);
            queue2.addLast(n2.right);
        }
        return queue1.isEmpty() && queue2.isEmpty();
    }
}
</pre>
