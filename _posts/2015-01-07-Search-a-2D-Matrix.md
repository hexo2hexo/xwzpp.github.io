---
layout: post
title:  LeetCode-Search a 2D Matrix
description: "Search a 2D Matrix"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Binary Search]
duoshuo: true
---
##题目
####Search a 2D Matrix
>Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
>
* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

>For example,

>Consider the following matrix:
>
	[
	  [1,   3,  5,  7],
	  [10, 11, 16, 20],
	  [23, 30, 34, 50]
	]

>Given **target** = `3`, return `true`. 

<!-- more -->
	
##解题思路
该题每一行的第一个元素要大于前一行的最后一个元素，且在行内是增序排列，这样在行上基本上是有序的。所以这里可以采用二分查找，首先对行进行二分查找，判断目标元素`target`在哪一行中，然后由于行内也是有序的，这样就可以对这一行使用二分查找，从而最终判断元素在不在矩阵中。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix==null || matrix.length==0 || matrix[0].length==0)
        	return false;
        int rownum=matrix.length;
        int colnum=matrix[0].length;
        //按行进行二分查找，确定在哪一行
        int rowi=0;
        int rowj=rownum-1;
        while(rowi<=rowj)
        {
        	int rowm=(rowi+rowj)/2;
        	if(matrix[rowm][0]<=target && target<=matrix[rowm][colnum-1])
        	{   //对这一行进行二分查找
        		int coli=0;
        		int colj=colnum-1;
        		while(coli<=colj)
        		{
        			int colm=(coli+colj)/2;
        			if(matrix[rowm][colm]==target)
        				return true;
        			else if(matrix[rowm][colm]<target){
        				coli=colm+1;
        			}else{
        				colj=colm-1;
        			}
        		}
        		return false;
        	}else if(matrix[rowm][0]>target){
        		rowj=rowm-1;
        	}else{
        		rowi=rowm+1;
        	}
        }
        return false;
    }
}
{% endhighlight %}

