---
layout: post
title:  LeetCode-Spiral Matrix
description: "Spiral Matrix"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array]
duoshuo: true
---
##题目
####Spiral Matrix
>Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

>For example,   
>Given the following matrix:
>
	[
	 [ 1, 2, 3 ],
	 [ 4, 5, 6 ],
	 [ 7, 8, 9 ]
	]

>You should return `[1,2,3,6,9,8,7,4,5]`.

<!-- more -->
	
##解题思路
基本思路跟[Rotate Image][1]有点类似，就是一层一层的处理，每一层都是按照右下左上的顺序进行读取就可以。实现中要注意两个细节，一个是因为题目中没有说明矩阵是不是方阵，因此要先判断一下行数和列数来确定螺旋的层数。另一个是因为一层会占用两行两列，如果是单数的，最后要将剩余的走完。所以最后还要做一次判断。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public ArrayList<Integer> spiralOrder(int[][] matrix) {
       	//按每一层进行输出
       	ArrayList<Integer> res=new ArrayList<Integer>();
       	if(matrix==null || matrix.length==0 ||matrix[0].length==0)
       		return res;
       	int row=matrix.length;
       	int col=matrix[0].length;
       	int min=Math.min(row,col);
        int cen=min/2;
       	for(int i=0;i<cen;i++)
       	{

       		for(int j=i;j<col-i-1;j++)
       			res.add(matrix[i][j]);
       		for(int j=i;j<row-i-1;j++)
       			res.add(matrix[j][col-i-1]);
       		for(int j=col-i-1;j>i;j--)
       			res.add(matrix[row-i-1][j]);
       		for(int j=row-i-1;j>i;j--)
       			res.add(matrix[j][i]);
       	}
       	
       	if(min%2==1)  
        {  
            if(row < col)  
            {  
                for(int j=cen; j<col-cen;j++)  
                {  
                    res.add(matrix[cen][j]);  
                }  
            }  
            else  
            {  
                for(int j=cen; j<row-cen;j++)  
                {  
                    res.add(matrix[j][cen]);  
                }  
            }  
        }  
       	return res;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Rotate-Image.html