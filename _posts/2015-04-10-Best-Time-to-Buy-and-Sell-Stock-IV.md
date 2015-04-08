---
layout: post
title:  LeetCode-Best Time to Buy and Sell Stock IV
description: "Best Time to Buy and Sell Stock IV"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming]
duoshuo: true
---
##题目
####Best Time to Buy and Sell Stock IV
>Say you have an array for which the ith element is the price of a given stock on day i.

>Design an algorithm to find the maximum profit. You may complete at most k transactions.

>####Note:
>You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

>####Credits:
>Special thanks to @Freezen for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
这道题与[Best Time to Buy and Sell Stock III][1]思路是一样的。这里同样采用动态规划进行求解，仍然使用局部最优和全局最优解法由于要考虑交易次数，因此维护量应该就是一个二维数组。

	定义维护量：
	global[i][j]:表示从第1天到第i天，最多交易j次的最好的利润
	local[i][j]:当前到达第i天，最多可进行j次交易，并且最后一次交易在当天卖出的最好的利润是多少
	定义递推式：
	global[i][j]=max(global[i-1][j],local[i][j]);即第i天没有交易，和第i天有交易
	local[i][j]=max(global[i-1][j-1]+max(diff,0),local[i-1][j]+diff)  diff=price[i]-price[i-1];
	就是看两个量，第一个是全局到i-1天进行j-1次交易，然后加上今天的交易，如果今天是赚钱的话（也就是前面只要j-1次交易，最后一次交易取当前天），第二个量则是取local第i-1天j次交易，然后加上今天的差值（这里因为local[i-1][j]比如包含第i-1天卖出的交易，所以现在变成第i天卖出，并不会增加交易次数，而且这里无论diff是不是大于0都一定要加上，因为否则就不满足local[i][j]必须在最后一天卖出的条件了）。
	需要注意的是：第i天卖出的交易数是算在前i-1天买入的那次交易中的。

需要注意的事，test case中，有一个非常大的k值，直接会让内存分配失败。

如何处理该种情况呢。 当k值超过prices值的个数时，此时，可以把问题转换为交易数次不限的情况。即

[Best Time to Buy and Sell Stock II][2]中的解法。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int maxProfit(int k, int[] prices) {
           if(prices==null || prices.length==0)
       		    return 0;
       		if(k>prices.length)
       		{
       			if(prices==null)
		            return 0;
		        int res=0;
		        for(int i=0;i<prices.length-1;i++)
		        {
		            int degit=prices[i+1]-prices[i];
		            if(degit>0)
		                res+=degit;
		        }
		        return res;
       		}
	        /*
	       定义维护量：
	       global[i][j]:表示从第1天到第i天，最多交易j次的最大利润
	       local[i][j]:表示第i天交易，最多交易次数为j次的最大利润，且最后一次肯定是在第i天卖出
	       定义递推式：
	       global[i][j]=max(global[i-1][j],local[i][j]);即第i天没有交易，和第i天有交易
	       local[i][j]=max(global[i-1][j-1]+max(diff,0),local[i-1][j]+diff)  diff=price[i]-price[i-1];
	        */
	        int[][] global=new int[prices.length][k+1];
	        int[][] local=new int[prices.length][k+1];
	        for(int i=0;i<prices.length-1;i++)
	        {
	            int diff=prices[i+1]-prices[i];
	            for(int j=0;j<=k-1;j++)
	            {
	                local[i+1][j+1]=Math.max(global[i][j]+Math.max(diff,0),local[i][j+1]+diff);
	                global[i+1][j+1]=Math.max(global[i][j+1],local[i+1][j+1]);
	            }
	        }
	        return global[prices.length-1][k];
	}
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Best-Time-to-Buy-and-Sell-Stock-III.html
[2]:http://pisxw.com/algorithm/Best-Time-to-Buy-and-Sell-Stock-II.html







