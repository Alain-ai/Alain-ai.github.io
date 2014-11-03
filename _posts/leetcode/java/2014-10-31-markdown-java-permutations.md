---
layout: post
title: LeetCode | Permutations in Java
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
    1. 方法1, in-place交换待排列列表
    2. 方法2, 使用"visited"和"stk"额外空间
*/
public class Permutations {

    public List<List<Integer>> permute(int [] num){
        List<Integer> numList = new ArrayList<Integer>(num.length);
        for (int i : num) numList.add(i);

        List<List<Integer>> res = new ArrayList<List<Integer>>();
        permuteRec(0, numList, res);
        return res;
    }

    private void permuteRec(int level, List<Integer> num, List<List<Integer>> res){
        if (level == num.size()) res.add(new ArrayList<Integer>(num));

        for (int i = level; i < num.size(); ++i){
            Collections.swap(num, i, level);
            permuteRec(level + 1, num, res);
            Collections.swap(num, i, level);
        }
    }


	public List<ArrayList<Integer>> permute(int[] num) {
        List<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
        Deque<Integer> stk = new ArrayDeque<Integer>();
        boolean[] visited;
		int len = num.length;
		visited = new boolean[len];
        permuteRec(0, num, res, stk, visited);
		return res;
	}

	public void permuteRec(int level, int[] num, List<ArrayList<Integer>> res, Deque<Integer> stk, boolean[] visited){
		if(level == num.length){
			res.add(new ArrayList<Integer>(stk));
			return;
		}
		for(int i = 0; i < num.length; ++i){
			if(!visited[i]){
				stk.addLast(num[i]);
				visited[i] = true;
                permuteRec(level + 1, num, res, stk, visited);
				visited[i] = false;
				stk.removeLast();
			}
		}
	}
}
</pre>
