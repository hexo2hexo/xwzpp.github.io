---
layout: post
title:  LeetCode-Surrounded Regions
description: "Surrounded Regions"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Breadth-first Search]
duoshuo: true
---
##题目
####Surrounded Regions
>Given a 2D board containing 'X' and 'O', capture all regions surrounded by 'X'.

>A region is captured by flipping all 'O's into 'X's in that surrounded region.

>For example,
>
	X X X X
	X O O X
	X X O X
	X O X X

>After running your function, the board should be:
>
	X X X X
	X X X X
	X X X X
	X O X X

<!-- more -->
	
##解题思路 
这个题目用到的方法是图形学中的一个常用方法：[Flood fill][1]算法，其实就是从一个点出发对周围区域进行目标颜色的填充。背后的思想就是把一个矩阵看成一个图的结构，每个点看成结点，而边则是他上下左右的相邻点，然后进行一次广度或者深度优先搜索。   

接下来我们看看这个题如何用[Flood fill][1]算法来解决。首先我们知道，如果从一个'O'出发，到达一个边缘的‘O’时，此时这条路是没有被包围的，这些‘O’都不会变为‘X’，而没有到达边缘的那些‘O’是需要变为‘X’的，因此边缘需要特殊处理。在这里，我们采用首先从边缘开始来fill,把所有边缘上‘O’能到的'O'都变为‘#’，这样再全局遍历一次整个矩阵，把‘#’变为‘O’，把‘O’变为‘X’即可。

这里采用广度优先所搜去找到从一个‘O’出发，能到达的所有‘O’的路径。

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public void solve(char[][] board) {
    	if(board==null || board.length<=1 || board[0].length<=1)  
       		return;  
        //对边缘进行搜索
        for(int i=0;i<board[0].length;i++)
        {
        	fill(board,0,i);
        	fill(board,board.length-1,i);
        }

        for(int i=0;i<board.length-1;i++)
        {
        	fill(board,i,0);
        	fill(board,i,board[0].length-1);
        }

        //最后遍历，把'#'变为‘O’，把‘O’变为‘X’
        for(int i=0;i<board.length;i++)
        {
        	for(int j=0;j<board[0].length;j++)
        	{
        		if(board[i][j]=='#')
        			board[i][j]='O';
        		else
        			board[i][j]='X';
        	}
        }
    }


    //进行广度搜索
    public void fill(char[][] board,int i,int j)
    {
    	if(board[i][j]!='O')
    		return;
    	board[i][j]='#';
    	//定义队列，进行广度优先遍历
    	LinkedList<Integer> queen=new LinkedList<Integer>();
    	queen.offer(i*board[0].length+j);
    	while(!queen.isEmpty())
    	{
    		Integer cur=queen.poll();
    		int row=cur/board[0].length;
    		int col=cur%board[0].length;
    		//向上
    		if(row>0 && board[row-1][col]=='O')
    		{
    			queen.offer((row-1)*board[0].length+col);
    			board[row-1][col]='#';
    		}
    		//向下
    		if(row<board.length-1 && board[row+1][col]=='O')
    		{
    			queen.offer((row+1)*board[0].length+col);
    			board[row+1][col]='#';
    		}
    		//向左
    		if(col>0 && board[row][col-1]=='O')
    		{
    			queen.offer((row)*board[0].length+col-1);
    			board[row][col-1]='#';
    		}
    		//向右
    		if(col<board[0].length-1 && board[row][col+1]=='O')
    		{
    			queen.offer((row)*board[0].length+col+1);
    			board[row][col+1]='#';
    		}
    	}
    }
}
{% endhighlight %}

[1]:http://zh.wikipedia.org/wiki/Flood_fill









