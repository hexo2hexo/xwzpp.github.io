---
layout: post
title:  LeetCode-Number of Islands
description: "Number of Islands"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Depth-first Search,Breadth-first Search]
duoshuo: true
---
##题目
####Number of Islands
>Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

>####Example 1:
>
	11110
	11010
	11000
	00000
>Answer: 1

>####Example 2:
>
	11000
	11000
	00100
	00011
>Answer: 3

>####Credits:
>Special thanks to @mithmatt for adding this problem and creating all test cases.
<!-- more -->
	
##解题思路
这道题其实本质上就是统计联通子图的个数，即从一个没有被访问的1出发，进行广度或者深度遍历，肯定能得到一个联通子图，即一个岛，那么通过查看有多少个联通子图即可，这里采用深度优先搜索，但是这里需要判断节点是否访问过。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int numIslands(char[][] grid) {
        if(grid==null || grid.length==0 || grid[0].length==0)
        	return 0;
        //使用深度优先搜索
        int rows=grid.length;
        int cols=grid[0].length;
        int res=0;
        boolean[][] isVisited=new boolean[rows][cols];
        for(int i=0;i<rows;i++)
        	for(int j=0;j<cols;j++)
        	{
        		if(isVisited[i][j]==false && grid[i][j]=='1')
        		{	
        			helper(grid,i,j,isVisited);
        			res++;
        		}
        			
        	}
        return res;
    }

    public void helper(char[][] grid,int row,int col,boolean[][] isVisited)
    {
    	//四个方面
    	isVisited[row][col]=true;
    	//上方
		if(row>0 && isVisited[row-1][col]==false && grid[row-1][col]=='1')
			helper(grid,row-1,col,isVisited);

		//下方
		if(row<grid.length-1 && isVisited[row+1][col]==false && grid[row+1][col]=='1')
			helper(grid,row+1,col,isVisited);

		//左方
		if(col>0 && isVisited[row][col-1]==false && grid[row][col-1]=='1')
			helper(grid,row,col-1,isVisited);

		//右方
		if(col<grid[0].length-1 && isVisited[row][col+1]==false && grid[row][col+1]=='1')
			helper(grid,row,col+1,isVisited);
    }
}
{% endhighlight %}










