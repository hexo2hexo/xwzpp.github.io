---
layout: post
title:  LeetCode-Unique Paths
description: "Unique Paths"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Dynamic Programming]
duoshuo: true
---
##题目
####Unique Paths
>A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

>The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

>How many possible unique paths are there?   
>![][1]

>Above is a `3 x 7` grid. How many possible unique paths are there?

>**Note**: `m` and `n` will be at most 100.

<!-- more -->
	
##解题思路
该题只能向前和向下走，这样右边和下边位置的路径条数依赖于前面，所以可以采用**动态规划**求解。

	定义dp[i][j]:表示从start到[i,j]位置的不同路径条数
	递推公式为：
	dp[i][j]=dp[i-1][j]+dp[i][j-1] //只有两个方向可以到达dp[i][j]
	由于第一行和第一列的位置只有唯一条路径，所以初始化为：
	dp[0][0]=1,dp[0][1]=1,.....dp[0][n-1]=1
	dp[0][0]=1,dp[1][0]=1,.....dp[m-1][0]=1

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp=new int[m][n]; //dp[i][j]表示从start到[i,j]位置不同路径条数
        for(int i=0;i<n;i++)
        	dp[0][i]=1;
        for(int j=0;j<m;j++)
        	dp[j][0]=1;
        for(int i=1;i<m;i++)
        	for(int j=1;j<n;j++)
        		dp[i][j]=dp[i-1][j]+dp[i][j-1];
        return dp[m-1][n-1];
    }
}
{% endhighlight %}

[1]:/img/Unique-Paths/1.png