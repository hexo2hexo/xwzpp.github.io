---
layout: post
title:  LeetCode-Climbing Stairs
description: "Climbing Stairs"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming]
duoshuo: true
---
##题目
####Climbing Stairs
>You are climbing a stair case. It takes n steps to reach to the top.

>Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

<!-- more -->
	
##解题思路
该题是典型的动态规划方法，由于每次只能夸`1`步或`2`步，则到达第`i`层的方法数只依赖于到达第`i-1`层和第`i-2`层的方法数，因此动态规划定义如下：

	定义dp[i]:到达第i层共有的方法数
	则dp[i]=dp[i-1]+dp[i-2]

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int climbStairs(int n) {
        if(n<0)
        	return 0;
        if(n==1)
        	return 1;
        int[] dp=new int[n+1];//dp[i]表示到达第i层共有的方法数
        dp[1]=1;
        dp[2]=2;
        for(int i=3;i<=n;i++)
        	dp[i]=dp[i-1]+dp[i-2];
        return dp[n];

    }
}
{% endhighlight %}

