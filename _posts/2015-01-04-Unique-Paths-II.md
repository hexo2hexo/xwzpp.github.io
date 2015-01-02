---
layout: post
title:  LeetCode-Unique Paths II
description: "Unique Paths II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Dynamic Programming]
duoshuo: true
---
##题目
####Unique Paths II
>Follow up for "Unique Paths":

>Now consider if some obstacles are added to the grids. How many unique paths would there be?

>An obstacle and empty space is marked as `1` and `0` respectively in the grid.

>For example,   
>There is one obstacle in the middle of a 3x3 grid as illustrated below.   
>
	[
	  [0,0,0],
	  [0,1,0],
	  [0,0,0]
	]

>The total number of unique paths is `2`.

Note: m and n will be at most 100.

<!-- more -->
	
##解题思路
该题是[Unique Paths][1]的扩展，思路类似，只是这边要处理障碍。动态规划的思路可以见那题。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    	if(obstacleGrid==null || obstacleGrid.length==0)
    		return 0;
    	int m=obstacleGrid.length;
    	int n=obstacleGrid[0].length;
        int[][] dp=new int[m][n]; //dp[i][j]表示从start到[i,j]位置不同路径条数
        for(int i=0;i<m;i++)
        	for(int j=0;j<n;j++)
        		dp[i][j]=0;
        for(int i=0;i<n;i++)   //第一行障碍处理
        {
        	if(obstacleGrid[0][i]!=1)
        		dp[0][i]=1;
        	else
        		break;
        }
        	
        for(int j=0;j<m;j++)   //第一列障碍处理
        {
        	if(obstacleGrid[j][0]!=1)
        		dp[j][0]=1;
        	else
        		break;
        }
        for(int i=1;i<m;i++)
        	for(int j=1;j<n;j++)
        	{
        		if(obstacleGrid[i][j]==1)   //如果该位置是障碍，则到达该点的路径条数为0
        			dp[i][j]=0;
        		else
        			dp[i][j]=dp[i-1][j]+dp[i][j-1];
        	}		
        return dp[m-1][n-1];
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Unique-Paths.html

