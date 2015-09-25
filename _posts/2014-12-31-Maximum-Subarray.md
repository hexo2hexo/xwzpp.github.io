---
layout: post
title:  LeetCode-Maximum Subarray
description: "Maximum Subarray"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Divide and Conquer,Array,Dynamic Programming]
duoshuo: true
---
##题目
####Maximum Subarray
>Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

>For example, given the array `[−2,1,−3,4,−1,2,1,−5,4]`,   
>the contiguous subarray `[4,−1,2,1]` has the largest sum = `6`.

>####More practice:
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

<!-- more -->
	
##解题思路
该题是典型的动态规划求解，可以定义局部最优和全局最优

	定义dp[i]:以i为结尾的最大连续字符串之和  局部最优
	dp[i]=max(dp[i-1]+A[i],A[i]) //需要考虑dp[i-1]是负的情况，这时候就不需要加上它了

	这样遍历之后将会得到所有节点，以其为结尾的最大连续字符串之和。此时可以定义全局最优

	定义dpglobal[i]：从0到i节点中最长连续字串之和  全局最优
	dpglobal[i]=max(dpglobal[i-1],dp[i]);

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int maxSubArray(int[] A) {
        if(A==null || A.length==0)
        	return 0;
        //dp[i]表示以i为结尾的最大连续字串之和  局部最优
        int[] dp=new int[A.length]; 
        //dpglobal[i]表示从0到i节点中最长连续字串之和  全局最优
       	int[] dpglobal=new int[A.length];
       	dp[0]=A[0];
       	dpglobal[0]=A[0];
        for(int i=0;i<A.length-1;i++)
        {
        	dp[i+1]=Math.max(dp[i]+A[i+1],A[i+1]);
        	dpglobal[i+1]=Math.max(dpglobal[i],dp[i+1]);
        }
        return dpglobal[A.length-1];
    }
}
{% endhighlight %}
