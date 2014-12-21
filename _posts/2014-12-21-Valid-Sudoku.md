---
layout: post
title:  LeetCode-Valid Sudoku
description: "SValid Sudoku"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table]
duoshuo: true
---
##题目
####Valid Sudoku
>Determine if a Sudoku is valid, according to:   
>[Sudoku Puzzles - The Rules][1].

>The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

>![][2]

>A partially filled sudoku which is valid.

>####Note:

>A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

<!-- more -->

##解题思路
该题是判断一个数独是不是合法的问题，数独合法的问题只需要考察以下三个条件：
	
	1. 每一行不会出现重复的数字，1-9数字每个只出现一次
	2. 每一列不会出现重复的数字，1-9数字每个只出现一次
	3. 每一个3*3小方格中应该包含1-9所有的数字，但不会出现重复的数字

因此只需要对上面三个条件进行判定就可以决定数独是不是合法。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public boolean isValidSudoku(char[][] board) {
        // Note: The Solution object is instantiated only once and is reused by each test case.
        
        int mx = board.length;
        int my = board[0].length;
        
        int x, y;
        
        for(x = 0; x < mx; x++){
            HashSet<Character> col = new HashSet<Character>();
            for(y = 0; y < my; y++){
                char c = board[x][y];
                if(c != '.'){
                    if(col.contains(c)) return false;
                    
                    col.add(c);
                } 
            }
        }
        
        for(y = 0; y < my; y++){
            HashSet<Character> row = new HashSet<Character>();
            for(x = 0; x < mx; x++){
                char c = board[x][y];
                if(c != '.'){
                    if(row.contains(c)) return false;
                    
                    row.add(c);
                } 
            }
        }
        
        for(x = 0; x < mx; x += 3){
            for(y = 0; y < my; y += 3){
                
                HashSet<Character> block = new HashSet<Character>();
                
                for(int offset = 0; offset < 9; offset++){
                    int ox = offset % 3;
                    int oy = offset / 3;
                    
                    char c = board[x + ox][y + oy];
                    if(c != '.'){
                        if(block.contains(c)) return false;
                    
                        block.add(c);
                    } 
                }
            }
        }
        
        return true;
    }
}
{% endhighlight %}

[1]:http://sudoku.com.au/TheRules.aspx
[2]:/img/SuDoKu/1.png