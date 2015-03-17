---
layout: post
title:  LeetCode-Best Time to Buy and Sell Stock III
description: "Best Time to Buy and Sell Stock III"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Dynamic Programming]
duoshuo: true
---
##题目
####Best Time to Buy and Sell Stock III
>Say you have an array for which the ith element is the price of a given stock on day i.

>Design an algorithm to find the maximum profit. You may complete at most two transactions.

>####Note:
>You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

<!-- more -->
	
##解题思路
这道题是[Best Time to Buy and Sell Stock][1]的扩展，这里要求只能进行两次交易，然而这里可以扩展为K次交易，应该思路是一样的，只是`k=2`而已。这里同样采用动态规划进行求解，仍然使用**局部最优和全局最优解法**由于要考虑交易次数，因此维护量应该就是一个二维数组。

	定义维护量：
	global[i][j]:表示从第1天到第i天，最多交易j次的最好的利润
	local[i][j]:当前到达第i天，最多可进行j次交易，并且最后一次交易在当天卖出的最好的利润是多少
	定义递推式：
	global[i][j]=max(global[i-1][j],local[i][j]);即第i天没有交易，和第i天有交易
	local[i][j]=max(global[i-1][j-1]+max(diff,0),local[i-1][j]+diff)  diff=price[i]-price[i-1];
	就是看两个量，第一个是全局到i-1天进行j-1次交易，然后加上今天的交易，如果今天是赚钱的话（也就是前面只要j-1次交易，最后一次交易取当前天），第二个量则是取local第i-1天j次交易，然后加上今天的差值（这里因为local[i-1][j]比如包含第i-1天卖出的交易，所以现在变成第i天卖出，并不会增加交易次数，而且这里无论diff是不是大于0都一定要加上，因为否则就不满足local[i][j]必须在最后一天卖出的条件了）。
	需要注意的是：第i天卖出的交易数是算在前i-1天买入的那次交易中的。

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public int maxProfit(int[] prices) {
        if(prices==null || prices.length==0)
        	return 0;
        /*
		定义维护量：
		global[i][j]:表示从第1天到第i天，最多交易j次的最大利润
		local[i][j]:表示第i天交易，最多交易次数为j次的最大利润，且最后一次肯定是在第i天卖出
		定义递推式：
		global[i][j]=max(global[i-1][j],local[i][j]);即第i天没有交易，和第i天有交易
		local[i][j]=max(global[i-1][j-1]+max(diff,0),local[i-1][j]+diff)  diff=price[i]-price[i-1];
        */
        int[][] global=new int[prices.length][3];
        int[][] local=new int[prices.length][3];
		for(int i=0;i<prices.length-1;i++)
		{
			int diff=prices[i+1]-prices[i];
			for(int j=0;j<=1;j++)
			{
				local[i+1][j+1]=Math.max(global[i][j]+Math.max(diff,0),local[i][j+1]+diff);
				global[i+1][j+1]=Math.max(global[i][j+1],local[i+1][j+1]);
			}
		}
		return global[prices.length-1][2];
    }
}
{% endhighlight %}









