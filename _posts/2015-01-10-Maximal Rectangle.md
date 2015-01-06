---
layout: post
title:  LeetCode-Maximal Rectangle
description: "Maximal Rectangle"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Hash Table,Stack,Dynamic Programming]
duoshuo: true
---
##题目
####Maximal Rectangle 
>Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing all ones and return its area.

<!-- more -->
	
##解题思路
这道题的解法灵感来自于[Largest Rectangle in Histogram][1]这道题，假设我们把矩阵沿着某一行切下来，然后把切的行作为底面，将自底面往上的矩阵看成一个直方图（histogram）。直方图的中每个项的高度就是从底面行开始往上1的数量。根据[Largest Rectangle in Histogram][1]我们就可以求出当前行作为矩阵下边缘的一个最大矩阵。接下来如果对每一行都做一次[Largest Rectangle in Histogram][1]，从其中选出最大的矩阵，那么它就是整个矩阵中面积最大的子矩阵。    
算法的基本思路已经出来了，剩下的就是一些节省时间空间的问题了。    
我们如何计算某一行为底面时直方图的高度呢？ 如果重新计算，那么每次需要的计算数量就是当前行数乘以列数。然而在这里我们会发现一些动态规划的踪迹，如果我们知道上一行直方图的高度，我们只需要看新加进来的行（底面）上对应的列元素是不是0，如果是，则高度是0，否则则是上一行直方图的高度加1。利用历史信息，我们就可以在线行时间内完成对高度的更新。     

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int maximalRectangle(char[][] matrix) {
        if(matrix==null || matrix.length==0 || matrix[0].length==0)
        	return 0;
        //以每一行最为低求解最大矩形面积
        int[] height=new int[matrix[0].length];
        int maxrec=0;
        for(int i=0;i<matrix.length;i++)
        {	
        	for(int j=0;j<matrix[0].length;j++)
        	{
				//对高度进行更新
        		if(matrix[i][j]=='1')
	        	{
	        		height[j]+=1;
	        	}else{
	        		height[j]=0;
	        	}
        	}
        	maxrec=Math.max(maxrec,largestRectangleArea(height));      	
        }
        return maxrec;
    }

    public int largestRectangleArea(int[] height) {
        if(height==null || height.length==0)
        	return 0;
        if(height.length==1)
        	return height[0];
        //使用栈来求解每个bar左边高度小于H(bar)的最大的x坐标，记为left
        int[] left=new int[height.length];
        LinkedList<Integer> stack=new LinkedList<Integer>();
        stack.push(0);
        for(int i=0;i<height.length;i++)
        {
        	while(stack.size()!=0 &&(height[stack.peek()]>=height[i]))
    		{
    			stack.pop();
    		}
    		if(stack.size()==0)
    		{
    			left[i]=-1;
    			stack.push(i);
    		}		
    		else
    		{
    			left[i]=stack.peek();
    			stack.push(i);
    		}	
        }

        //同理使用栈来求解每个bar右边高度小于H(bar)的最小的x坐标，记为right
        int[] right=new int[height.length];
        LinkedList<Integer> stack2=new LinkedList<Integer>();
        stack2.push(height.length-1);
        for(int i=height.length-1;i>=0;i--)
        {
        	while(stack2.size()!=0 &&(height[stack2.peek()]>=height[i]))
    		{
    			stack2.pop();
    		}
    		if(stack2.size()==0)
    		{
    			right[i]=height.length;
    			stack2.push(i);
    		}   			
    		else
    		{
    			right[i]=stack2.peek();
    			stack2.push(i);
    		}	
    	}

    	//计算每个bar能形成的矩形的面积，并求得一个最大面积
    	int maxRec=0;
    	for(int i=0;i<height.length;i++)
    	{
    		int rec=(right[i]-left[i]-1)*height[i];
    		maxRec=Math.max(maxRec,rec);
    	}
    	return maxRec;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Largest-Rectangle-in-Histogram.html

