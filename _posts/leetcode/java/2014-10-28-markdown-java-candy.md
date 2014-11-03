---
layout: post
title: LeetCode | Candy in Java
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
    1. 正反两面扫描
    2. candies初始先全部置1
    3. 正面扫描处理右边rating高的情况
    4. 反面扫描处理左边rating高的情况
*/
public class Candy{

    public int candy(int[] ratings) {
        if(ratings == null || ratings.length == 0) return 0;
        if(ratings.length == 1) return 1;

        int L = ratings.length;
        int [] candies = new int [L];
        Arrays.fill(candies, 1);

        for(int i = 1; i < L; ++i){
            if(ratings[i] > ratings[i-1]){
                candies[i] = candies[i-1] + 1;
            }
        }

        for(int i = L - 1; i >= 1; --i){
            if(ratings[i-1] > ratings[i] && candies[i-1] <= candies[i]){
                candies[i-1] = candies[i] + 1;
            }
        }

        int res = 0;
        for(int i = 0; i < L; ++i) res += candies[i];
        return res;
    }
}
</pre>
