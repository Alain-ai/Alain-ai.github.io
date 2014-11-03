---
layout: post
title: LeetCode | Combinations in Java
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
    DFS
*/
public class Combinations {

	public ArrayList<ArrayList<Integer>> combine(int n, int k) {
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
        combineRec(res, new ArrayDeque<Integer>(), k, n, 1);
		return res;
	}

	public void combineRec(ArrayList<ArrayList<Integer>> res, Deque<Integer> tmp, int left, int n, int s) {
		if (left == 0) {
			res.add(new ArrayList<Integer>(tmp));
		}
		for(int i = s; i <= n; ++i){
            tmp.addLast(i);
            combineRec(res, tmp, left-1, n, i+1);
            tmp.removeLast();
		}
	}
}
</pre>
