---
layout: post
title: LeetCode | N-Queens II in Java
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
    1. 检查列占用情况的所有排列
*/
public class N_Queens_II {

    int res = 0;

    public int totalNQueens(int n){
        List<Integer> perm = new ArrayList<Integer>(n);
        for (int i = 0; i < n; ++i) perm.add(i);
        totalNQueensRec(0, perm);
        return res;
    }

    private void totalNQueensRec(int level, List<Integer> perm){
        if (level == perm.size() && isValid(perm)) ++res;
        for (int i = level; i < perm.size(); ++i){
            Collections.swap(perm, i, level);
            totalNQueensRec(level + 1, perm);
            Collections.swap(perm, i, level);
        }
    }

    private boolean isValid(List<Integer> perm){
        for (int i = 0; i < perm.size(); ++i){
            for (int j = i + 1; j < perm.size(); ++j){
                if (i - j == perm.get(i) - perm.get(j) || i - j == perm.get(j) - perm.get(i)) return false;
            }
        }
        return true;
    }
}
</pre>
