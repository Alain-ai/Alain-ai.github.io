---
layout: post
title: LeetCode | Letter Combinations of a Phone Number in Java
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
    1. DFS
*/
public class Letter_Combinations_of_a_Phone_Number{

	String [] map = new String[]{"0","1","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};

	public ArrayList<String> letterCombinations(String digits) {
		return letterCombinationsRec(digits);
	}

	public ArrayList<String> letterCombinationsRec(String digits) {
		ArrayList<String> res = new ArrayList<String>();
		if(digits.isEmpty()) {
			res.add("");
            return res;
		}
		char c = digits.charAt(0);
		String metas = map[c-'0'];
		ArrayList<String> subRes = letterCombinationsRec(digits.substring(1));
		for(int i = 0 ; i < metas.length(); ++i){
			for(String sub : subRes){
				res.add(metas.charAt(i) + sub);
			}
		}
		return res;
	}
}
</pre>
