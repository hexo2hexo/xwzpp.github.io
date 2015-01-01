---
layout: post
title:  LeetCode-Spiral Matrix II
description: "Spiral Matrix II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array]
duoshuo: true
---
##题目
####Spiral Matrix II
>Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

>For example,   
>Given n = 3,

>You should return the following matrix:
>
	[
	 [ 1, 2, 3 ],
	 [ 8, 9, 4 ],
	 [ 7, 6, 5 ]
	]

<!-- more -->
	
##解题思路
该题与[Spiral Matrix][1]类似，`Spiral Matrix`是按螺旋序输出矩阵中的元素，但是其中矩阵不一定是方阵，该题是对方阵中进行螺旋序的填充数字，具体解法基本类似，但是这里需要注意一点，如果`n`为奇数，不要忘记最后一层是一个独立元素。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int[][] generateMatrix(int n) {
    	int[][] res=new int[n][n];
        if(n==0)
        	return res;
    	int num=1;
        int cen=n/2;
        for(int i=0;i<cen;i++)
        {
        	for(int j=i;j<n-i-1;j++) //上
        		res[i][j]=(num++);
        	for(int j=i;j<n-i-1;j++)  //右
        		res[j][n-i-1]=(num++);
        	for(int j=n-i-1;j>i;j--)  //下
                res[n-i-1][j]=(num++);
            for(int j=n-i-1;j>i;j--)  //左
                res[j][i]=(num++);
        }

        if(n%2==1)  
       		res[cen][cen]=(num++);
       	return res;
    }
} 
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Spiral-Matrix.html