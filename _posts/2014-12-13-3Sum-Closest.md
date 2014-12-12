---
layout: post
title:  LeetCode-3Sum Closest
description: "3Sum Closest"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Two Pointers]
duoshuo: true
---
##题目
####3Sum Closest

>Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
>
	For example, given array S = {-1 2 1 -4}, and target = 1.
>
    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).



<!-- more -->

##解题思路
该题是求解是找到三个数的和，使得该和最接近给定的目标值。因为`a+b+c`的和最接近`target`,可以看成是`b+c`的最接近于`target-a`,这样三个数的问题就可以变为两个数的问题。而两个数的问题可以采用**左右夹逼**法进行求解，当然这个前提是数组必须是排好序的。时间复杂度为`O(n^2+nlogn)`,即`O(n^2)`。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
	//a+b+c的和接近target,可以认为b+c的和接近target-a,这样使得三个数变成两个数的问题
    public int threeSumClosest(int[] num, int target) {
        Arrays.sort(num);
        if(num.length<=2)
            return 0;
       	int closestsum=num[0]+num[1]+num[2]; //维持一个最接近target的和
       	for(int i=0;i<num.length-2;i++)
       	{
       		int twosum=twoSumClosest(num,i+1,target-num[i]);
       		if(Math.abs(num[i]+twosum-target)<Math.abs(closestsum-target))
       			closestsum=num[i]+twosum;
       	}
       	return closestsum;
    }

    public int twoSumClosest(int[] num,int start,int target)
    {
    	int i=start;
    	int j=num.length-1;
    	int closestsum=num[i]+num[i+1]; //维持一个最接近target的和
    	while(i<j)
    	{
    		if(Math.abs(num[i]+num[j]-target)<Math.abs(closestsum-target))
    			closestsum=num[i]+num[j];
    		if((num[i]+num[j])>target)
    			j--;
    		else
    			i++;
    	}
    	return closestsum;
    }
}
{% endhighlight %}

