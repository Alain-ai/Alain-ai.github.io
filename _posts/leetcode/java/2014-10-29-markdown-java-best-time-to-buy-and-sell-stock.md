---
layout: post
title: LeetCode | Best Time to Buy and Sell Stock in Java
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
    1. 分治法，记录前后两个部分的最大最小值
    2. 对于一个位置，记录它前面的最小值
    3. 转化为最大连续子数组和
*/
public class Best_Time_to_Buy_and_Sell_Stock {

	public int maxProfit(int[] prices) {
		return maxProfitRec(prices, 0, prices.length - 1, new int [] {0 , 0});
	}

	public int maxProfitRec(int[] prices, int s, int e, int [] maxmin) {
		if (s >= e) {
            Arrays.fill(maxmin, prices[s]);
            return 0;
        }
		if (e - s == 1) {
			int diff = prices[e] - prices[s];
            maxmin[0] = Math.max(prices[s], prices[e]);
            maxmin[1] = Math.min(prices[s], prices[e]);
			return diff >= 0 ? diff : 0;
		}
		int mid = (e + s) >>> 1;
		int diff1 = maxProfitRec(prices, s, mid, maxmin);
        int max0 = maxmin[0], min0 = maxmin[1];
		int diff2 = maxProfitRec(prices, mid + 1, e, maxmin);
        int max1 = maxmin[0], min1 = maxmin[1];
		int diff = max1 - min0;
        maxmin[0] = Math.max(max0, max1);
        maxmin[1] = Math.min(min0, min1);
		return Math.max(diff, Math.max(diff1, diff2));
	}


	public int maxProfit2(int[] prices) {
		if(prices == null || prices.length <= 1) return 0;
		int maxProfit = 0;
		int curMin = prices[0];
		for(int i = 0; i < prices.length; ++i){
			if(prices[i] - curMin > maxProfit){
				maxProfit = prices[i] - curMin;
			}
			if(prices[i] < curMin){
				curMin = prices[i];
			}
		}
		return maxProfit;
	}


    public int maxProfit3(int [] prices){
        if(prices == null || prices.length <= 1) return 0;
        int [] diff = new int [prices.length - 1];
        for (int i = 0; i < prices.length - 1; ++i){
            diff[i] = prices[i+1] - prices[i];
        }
        int [] DP = new int[diff.length];
        DP[0] = diff[0] >= 0? diff[0] : 0;
        for (int i = 1; i < diff.length; ++i){
              if (DP[i-1] + diff[i] >= 0){
                  DP[i] = DP[i-1] + diff[i];
              }else {
                  DP[i] =diff[i] >= 0? diff[i] : 0;
              }
        }
        int max = 0;
        for (int i : DP){
            max = Math.max(i, max);
        }
        return max;
    }
}
</pre>
