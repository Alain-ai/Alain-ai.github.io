---
layout: post
title: LeetCode | Convert Sorted List to Binary Search Tree in Java
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
    1. 两步法在linkedlist中找中间点
*/
public class Convert_Sorted_List_to_Binary_Search_Tree {

	public TreeNode sortedListToBST(ListNode head) {
		return sortedListToBSTRec(head);
	}

	public TreeNode sortedListToBSTRec(ListNode head){
		if(head == null) return null; // length 0 list
		if(head.next == null) return new TreeNode(head.val); // length 1 list
		if(head.next.next == null){ // length 2 list
			TreeNode t =  new TreeNode(head.val);
			TreeNode t1 =  new TreeNode(head.next.val);
			t.right = t1;
			return t;
		}
        // length more than 2 list
		ListNode dummy = new ListNode(0);
		dummy.next = head;
		ListNode pp = dummy, p = head;
        // 2 stepsize trick to find middle node
		while(p != null && p.next != null){
			pp = pp.next;
			p = p.next.next;
		}
		ListNode h1 = head;
		ListNode h2 = pp.next.next;
		TreeNode t = new TreeNode(pp.next.val);
		pp.next = null; // Note to set null
		TreeNode t1 = sortedListToBSTRec(h1);
		TreeNode t2 = sortedListToBSTRec(h2);
		t.left = t1;
		t.right = t2;
		return t;
	}
}
</pre>
