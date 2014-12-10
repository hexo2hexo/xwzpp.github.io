---
layout: post
title:  LeetCode-Container With Most Water
description: "Container With Most Water"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Two Pointers]
duoshuo: true
---
##题目
####Container With Most Water

>Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

>Note: You may not slant the container.



<!-- more -->

##解题思路
该题是求解最大的容积问题，如果我们采用“暴力法”求解，则每一对pair都需要计算一次容积，然后获得最大的那个，时间复杂度为`O(n^2)`。    
因此需要对其进行优化，这里我们可以采用**左右夹逼**法求解，从数组两端开始，分别设置左指针`pLeft`和右指针`pRight`,然后比较`pLeft`和`pRight`哪个数值大，假设`pLeft`小，则如果向左移动`pRight`,出现的容积不可能比现在好，因为瓶颈在`pLeft`处，所以只有向右移动`pLeft`,才可能出现更大的容积。当然，在这个左右移动指针的过程中，需要维护一个最大的容积。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
	//采用左右夹逼法
    public int maxArea(int[] height) {
        int len=height.length;
        if(len<=1) return 0;
        int maxarea=Integer.MIN_VALUE;
        int i=0;
        int j=len-1;
        while(i<j)
        {
        	int area=Math.abs(i-j)*Math.min(height[i],height[j]);
        	if(area>maxarea)
        		maxarea=area;
        	if(height[i]<height[j])
        		i++;
        	else
        		j--;
        }
        return maxarea;
    }
}
{% endhighlight %}

