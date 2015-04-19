---
layout: post
title:  LeetCode-House Robber
description: "House Robber"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming]
duoshuo: true
---
##题目
####House Robber
>You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

>Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

>####Credits:
>Special thanks to @ifanchu for adding this problem and creating all test cases. Also thanks to @ts for adding additional test cases.

<!-- more -->
	
##解题思路
这道题的本质相当于在一列数组中取出一个或多个不相邻数，使其和最大。 
这是一道动态规划问题。 
我们维护一个一位数组dp，其中dp[i]表示到i位置时不相邻数能形成的最大和。 
状态转移方程：

	dp[0] = num[0] （当i=0时）
	dp[1] = max(num[0], num[1]) （当i=1时）
	dp[i] = max(num[i] + dp[i - 2], dp[i - 1])   （当i !=0 and i != 1时）(num[i]抢还是不抢两种情况)

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int rob(int[] num) {
        //定义dp[i]表示抢到第i个房间的时候没有惊动警察的最大钱数
        if(num==null || num.length==0)
        	return 0;
        if(num.length==1)
        	return num[0];
        int[] dp=new int[num.length];
        dp[0]=num[0];
        dp[1]=Math.max(num[0],num[1]);
        for(int i=2;i<num.length;i++)
        	dp[i]=Math.max(dp[i-1],dp[i-2]+num[i]);
        return dp[num.length-1];
    }
}
{% endhighlight %}










