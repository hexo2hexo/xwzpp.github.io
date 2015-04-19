---
layout: post
title:  LeetCode-Sudoku Solver
description: "Sudoku Solver"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Backtracking]
duoshuo: true
---
##题目
####Sudoku Solver
>Write a program to solve a Sudoku puzzle by filling the empty cells.

>Empty cells are indicated by the character `'.'`.

>You may assume that there will be only one unique solution.

>![][1]

>A sudoku puzzle...

>![][2]

>...and its solution numbers marked in red.
<!-- more -->

##解题思路
该题是求解数独问题，思路就是循环处理子问题，对于每个格子，带入不同的9个数，然后判合法，如果成立就递归继续，结束后把数字设为空。其中每个格子中不同的元素相当于一个状态，这样可以看成是一个状态转换问题，可以采用**深度优先搜索**进行求解。   
判合法可以用Valid Sudoku做为subroutine，但是其实在这里因为每次进入时已经保证之前的board不会冲突，所以不需要判断整个盘，只需要看当前加入的数字的行，列和方格中是否合法即可。这样可以大大提高运行效率，毕竟判合法在程序中被多次调用。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public void solveSudoku(char[][] board) {
    if(board == null || board.length != 9 || board[0].length !=9)
        return;
    helper(board,0,0);
    }
    private boolean helper(char[][] board, int i, int j)
    {
        if(j>=9)
            return helper(board,i+1,0);
        if(i==9)
        {
            return true;
        }
        if(board[i][j]=='.')
        {
            for(int k=1;k<=9;k++)
            {
                board[i][j] = (char)(k+'0');
                if(isValid(board,i,j))
                {
                    if(helper(board,i,j+1))
                        return true;
                }
                board[i][j] = '.';
            }
        }
        else
        {
            return helper(board,i,j+1);
        }
        return false;
    }
    private boolean isValid(char[][] board, int i, int j)
    {
        for(int k=0;k<9;k++)
        {
            if(k!=j && board[i][k]==board[i][j])
                return false;
        }
        for(int k=0;k<9;k++)
        {
            if(k!=i && board[k][j]==board[i][j])
                return false;
        }        
        for(int row = i/3*3; row<i/3*3+3; row++)
        {
            for(int col=j/3*3; col<j/3*3+3; col++)
            {
                if((row!=i || col!=j) && board[row][col]==board[i][j])
                    return false;
            }
        }
        return true;
    }
}
{% endhighlight %}

[1]:/img/SuDoKu/2.png
[2]:/img/SuDoKu/3.png