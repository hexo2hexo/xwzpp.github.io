---
layout: post
title:  LeetCode-Rotate Image 
description: "Rotate Image"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array]
duoshuo: true
---
##题目
####Rotate Image
>You are given an n x n 2D matrix representing an image.

>Rotate the image by 90 degrees (clockwise).

>Follow up:

>Could you do this in-place?

<!-- more -->
	
##解题思路
基本思路是把图片分为行数/2层，然后一层层进行旋转，每一层有上下左右四个列，然后目标就是把上列放到右列，右列放到下列，下列放到左列，左列放回上列，中间保存一个临时变量即可。

例如这张图：
![][1]

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public void rotate(int[][] matrix) {
        if(matrix==null)
        	return;
        int n=matrix.length-1;
        for (int i = 0; i <= n/2; ++i)    
        {    
            for (int j = i; j < n-i; ++j)    
            {    
                int tmp = matrix[i][j];    
                matrix[i][j] = matrix[n-j][i];    
                matrix[n-j][i] = matrix[n-i][n-j];    
                matrix[n-i][n-j] = matrix[j][n-i];    
                matrix[j][n-i] = tmp;    
            }    
        }    
    }
}
{% endhighlight %}

[1]:/img/Rotate-Image/1.jpg