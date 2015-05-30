---
layout: post
title:  LeetCode-House Robber II
description: "House Robber II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming]
duoshuo: true
---
##题目
####House Robber II
>Note: This is an extension of House Robber.

>After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are **arranged in a circle**. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

>Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

>####Credits:
>Special thanks to @Freezen for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
该题是在[House Robber][1]上的扩展，将上题中的直线型的街道，变成环形的街道，但是我们可以用线性街道的动态规划的方法求解。

对于环形，主要考虑两种情况：
+ 第一个房子被偷：那么此时第二个房子和最后一个房子都不能被偷了，即我们可以从第三个房子到倒数最后一个房子之间用线性的动态规划求解。
+ 第一个房子没有被偷：那么此时我们可以从第二个房子到最后一个房子之间用线性的动态规划求解。

具体动态方程为：

	设定：dp[i]:表示抢到第i个房间的时候没有惊动警察的最大钱数
	第一个房子被偷：
		dp1[0]=nums[0];
		dp1[1]=nums[0];
		dp1[i]=Max(dp1[i-2]+nums[i],dp1[i-1])   2<=i<=nums.length-2
		dp1[nums.length-1]=dp1[nums.length-2]

	第一个房子没有被偷：
		dp2[0]=0;
		dp2[1]=nums[1];
		dp2[i]=Max(dp2[i-2]+nums[i],dp2[i-1])   2<=i<=nums.length-1

	最后的结果为 Max(dp1[nums.length-1],dp2[nums.length-1])

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int rob(int[] nums) {
        if(nums==null || nums.length==0) return 0;
        //第一个房子没有被偷，则可以从第二个房子偷到最后一个房子，在这之间用线性的动态规划求解
        //dp[i]表示到第i个房子，小偷没用惊动警察时获取的最大钱数
        int[] dp1=new int[nums.length];
        dp1[0]=0;
        dp1[1]=nums[1];
        for(int i=2;i<nums.length;i++)
        	dp1[i]=Math.max(dp1[i-2]+nums[i],dp1[i-1]);

        //第一个房子被偷，则第二个和最后一个房子不能被偷，则从第三个房子到倒数最后一个房子之间用线性动态规划求解
        int[] dp2=new int[nums.length];
        dp2[0]=nums[0];
        dp2[1]=nums[0];
        for(int i=2;i<nums.length-1;i++)
        	dp2[i]=Math.max(dp2[i-2]+nums[i],dp2[i-1]);
        dp2[nums.length-1]=dp2[nums.length-2];

        return Math.max(dp1[nums.length-1],dp2[nums.length-1]);
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/House-Robber.html














