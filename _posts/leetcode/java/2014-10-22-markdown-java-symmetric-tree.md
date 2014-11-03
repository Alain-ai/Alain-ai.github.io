---
layout: post
title: LeetCode | Symmetric Tree in Java
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
    1. BFS 迭代解法
    2. DFS 递归解法
*/
public class Symmetric_Tree {

    public boolean isSymmetric(TreeNode root) {
//        if(root == null) return true;
//          return isSymmetricRec(root.left, root.right);
        return isSymmetricItr(root);
    }

    public boolean isSymmetricItr(TreeNode root){
        ArrayDeque<TreeNode> queue1 = new ArrayDeque<TreeNode>();
        ArrayDeque<TreeNode> queue2 = new ArrayDeque<TreeNode>();
        queue1.offerLast(root);
        queue2.offerLast(root);

        while(!queue1.isEmpty() && !queue2.isEmpty()){
            TreeNode n1 = queue1.pollFirst();
            TreeNode n2 = queue2.pollFirst();

            if(n1 == null && n2 == null) continue;
            if(n1 == null || n2 == null) return false;
            if(n1.val != n2.val) return false;

            queue1.offerLast(n1.left);
            queue1.offerLast(n1.right);

            queue2.offerLast(n2.right);
            queue2.offerLast(n2.left);
        }
        return queue1.isEmpty() && queue2.isEmpty();
    }

    public boolean isSymmetricRec(TreeNode t1, TreeNode t2){
        if((t1 == null && t2 != null) || (t1 != null && t2 == null))
            return false;
        if(t1 == t2) return true;
        if(t1.val != t2.val) return false;
        TreeNode tmp1 = t1.left;
        TreeNode tmp2 = t2.right;
        if(!isSymmetricRec(tmp1, tmp2)) return false;
        tmp1 = t1.right;
        tmp2 = t2.left;
        return isSymmetricRec(tmp1, tmp2);
    }
}
</pre>
