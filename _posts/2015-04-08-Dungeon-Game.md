---
layout: post
title:  LeetCode-Dungeon Game
description: "Dungeon Game"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming,Binary Search]
duoshuo: true
---
##题目
####Dungeon Game
>The demons had captured the princess (P) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight (K) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

>The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

>Some of the rooms are guarded by demons, so the knight loses health (negative integers) upon entering these rooms; other rooms are either empty (0's) or contain magic orbs that increase the knight's health (positive integers).

>In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.


>####Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.

>For example, given the dungeon below, the initial health of the knight must be at least 7 if he follows the optimal path `RIGHT-> RIGHT -> DOWN -> DOWN`.
>
	-2 (K)	-3	   3
	-5	    -10	   1
	10	    30	  -5 (P)

>####Notes:
>
+ The knight's health has no upper bound.
+ Any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.
>####Credits:
>Special thanks to @stellari for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
这题容易想到的思路是用search DFS或者BFS解，给定起点和终点，我们可以搜索所有从起点到终点的路径，然后贪心保存下来最小的路径权值之和，同时要保证每次扩展分支时当前的生命值状态始终大于0。但是这并不是好的解法，时间复杂度太高。    
该道题由于只能向右和向下移动，因此可以采用动态规划求解，是一个典型的二维动态规划问题，我们可以如下定义：

	对于从（0,0）点走到（m-1,n-1)
	dp[i][j]:表示从（i,j）走到（m-1.n-1）所需的最小生命值
	递推式为：
	dp[i][j]=max(min(dp[i+1][j],dp[i][j+1])-dungeon[i][j],0)
	如果dungeon[i][j]为正，则减去一个正数，初始需要的生命值变小。同理可以理解dungeon[i][j]为负数的情况。和0取最大保证了初始生命值为非负。
迭代的方法是初始化后，从下往上，从右往左进行填表。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        if(dungeon==null)
        	return -1;
        int m=dungeon.length;//行数
        int n=dungeon[0].length;//列数
        int[][] dp=new int[m][n];

        //对m-1行和n-1列进行初始化
        dp[m-1][n-1]=Math.max(0-dungeon[m-1][n-1],0);
        for(int i=n-2;i>=0;i--)
        {
        	dp[m-1][i]=Math.max(dp[m-1][i+1]-dungeon[m-1][i],0);
        }

        for(int i=m-2;i>=0;i--)
        {
        	dp[i][n-1]=Math.max(dp[i+1][n-1]-dungeon[i][n-1],0);
        }

        //进行填表
        for(int i=m-2;i>=0;i--)
        {
        	for(int j=n-2;j>=0;j--)
        	{
        		dp[i][j]=Math.max(Math.min(dp[i+1][j],dp[i][j+1])-dungeon[i][j],0);
        	}

        }

        return dp[0][0]+1;
    }
}
{% endhighlight %}








