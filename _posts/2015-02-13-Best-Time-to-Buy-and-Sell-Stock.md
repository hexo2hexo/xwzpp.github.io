---
layout: post
title:  LeetCode-Best Time to Buy and Sell Stock
description: "Best Time to Buy and Sell Stock"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Dynamic Programming]
duoshuo: true
---
##题目
####Best Time to Buy and Sell Stock
>Say you have an array for which the ith element is the price of a given stock on day i.

>If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

<!-- more -->
	
##解题思路
这道题求进行一次交易能得到的最大利润。如果用`brute force`的解法就是对每组交易都看一下利润，取其中最大的，总用有n*(n-1)/2个可能交易，所以复杂度是O(n^2)。       
很容易感觉出来这是动态规划的题目,用“局部最优和全局最优解法”。思路是维护两个变量，一个是到目前为止最好的交易，另一个是在当前一天卖出的最佳交易（也就是局部最优）。递推式是

	local[i]:表示在第i天卖出的最佳交易
	global[i]:表示从第1天开始到第i天的最好交易
	local[i+1]=max(local[i]+prices[i+1]-price[i],0)
	global[i+1]=max(local[i+1],global[i])

这样一次扫描就可以得到结果，时间复杂度是O(n)。

##算法代码
代码采用JAVA实现： 
{% highlight java %}
 public class Solution {
    public int maxProfit(int[] prices) {
        if(prices==null)
        	return 0;
        //定义局部最优维护量
        int local=0;
        //定义全局最优维护量
        int global=0;
        for(int i=0;i<prices.length-1;i++)
        {
        	local=Math.max(0,local+prices[i+1]-prices[i]);
        	global=Math.max(global,local);
        }
        return global;
    }
}
{% endhighlight %}









