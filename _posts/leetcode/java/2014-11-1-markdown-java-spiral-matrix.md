---
layout: post
title: LeetCode | Spiral Matrix  in Java
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
    1. 行列分别向中间靠拢
*/
public class Spiral_Matrix{

    public ArrayList<Integer> spiralOrder(int[][] matrix) {
        ArrayList<Integer> res = new ArrayList<Integer>();
        if(matrix.length == 0 || matrix[0].length == 0) return res;
        int c1 = 0, c2 = matrix[0].length-1, r1 = 0, r2 = matrix.length - 1;
        while(valid(r1, r2, c1, c2)){
            for(int i = c1; i <= c2; ++i){
                res.add(matrix[r1][i]);
            }
            if (!valid(++r1, r2, c1, c2)) break;
            for(int i = r1; i <= r2; ++i){
                res.add(matrix[i][c2]);
            }
            if (!valid(r1, r2, c1, --c2)) break;
            for(int i = c2; i >= c1; --i){
                res.add(matrix[r2][i]);
            }
            if(!valid(r1, --r2, c1, c2)) break;
            for(int i = r2; i >= r1; --i){
                res.add(matrix[i][c1]);
            }
            if(!valid(r1, r2, ++c1, c2)) break;
        }
        return res;
    }

    private boolean valid(int r1, int r2, int c1, int c2){
        return c1 <= c2 && r1 <= r2;
    }
}
</pre>
