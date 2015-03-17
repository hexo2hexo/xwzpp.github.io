---
layout: post
title:  LeetCode-Best Time to Buy and Sell Stock II
description: "Best Time to Buy and Sell Stock II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Greedy]
duoshuo: true
---
##题目
####Best Time to Buy and Sell Stock II
>Say you have an array for which the ith element is the price of a given stock on day i.

>Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

<!-- more -->
	
##解题思路
这道题跟[Best Time to Buy and Sell Stock][1]类似，求最大利润。区别是这里可以交易无限多次（当然我们知道交易不会超过n-1次，也就是每天都进行先卖然后买）。既然交易次数没有限定，可以看出我们只要对于每次两天差价大于0的都进行交易，就可以得到最大利润。因此算法其实就是累加所有大于0的差价既可以了，非常简单。如此只需要一次扫描就可以了

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public int maxProfit(int[] prices) {
        //该题由于可以无限次数的买入卖出，所以最大利润应该就是相邻两天差价不为0的利润之和
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
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Best-Time-to-Buy-and-Sell-Stock.html








