---
layout: post
title:  LeetCode-Minimum Path Sum
description: "Minimum Path Sum"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Dynamic Programming]
duoshuo: true
---
##题目
####Minimum Path Sum
>Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

>**Note**: You can only move either down or right at any point in time.

<!-- more -->
	
##解题思路
该题与[Unique Paths][1]非常类似，不过该题是求一条最短路径。同样采用**动态规划**求解：

	定义dp[i][j]:表示从左上点到[i,j]点所有路径中的最小和
	由于只能向下和向右移动，所以[i,j]的最小路径只依赖于[i-1,j]和[i,j-1]两个位置
	即dp[i][j]=min(dp[i-1][j]，dp[i][j-1])+grid[i][j]
	但是第一行和第一列要特殊处理。	


##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int minPathSum(int[][] grid) {
        if(grid==null || grid.length==0)
        	return 0;
        int m=grid.length;
        int n=grid[0].length;
        int[][] dp=new int[m][n]; //dp[i][j]表示从左上点到[i,j]点所有路径的最小和
        dp[0][0]=grid[0][0];
        for(int i=1;i<n;i++)  //初始化第一行
        	dp[0][i]=dp[0][i-1]+grid[0][i]; 
        for(int i=1;i<m;i++)  //初始化第一列
        	dp[i][0]=dp[i-1][0]+grid[i][0];
        for(int i=1;i<m;i++)
        	for(int j=1;j<n;j++)
        		dp[i][j]=Math.min(dp[i-1][j],dp[i][j-1])+grid[i][j];
        return dp[m-1][n-1]; 
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Unique-Paths.html
