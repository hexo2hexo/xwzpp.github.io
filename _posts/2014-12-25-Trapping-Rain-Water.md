---
layout: post
title:  LeetCode-Trapping Rain Water 
description: "Trapping Rain Water"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Stack,Two Pointers]
duoshuo: true
---
##题目
####Trapping Rain Water 
>Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

>For example, 
>Given `[0,1,0,2,1,0,1,3,2,1,2,1]`, return `6`.

>![][1]

>The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. Thanks Marcos for contributing this image!

<!-- more -->
	
##解题思路
该题与[Candy][2]类似，挨个分析每个A[i]能trapped water的容量，然后将所有的A[i]的trapped water容量相加即可。

其次，对于每个A[i]能trapped water的容量，取决于A[i]左右两边的高度（可延展）较小值与A[i]的差值，即volume[i] = [min(left[i], right[i]) - A[i]] * 1，这里的1是宽度，如果the width of each bar is 2,那就要乘以2了”

那么如何求A[i]的左右高度呢？ 要知道，能盛多少水主要看短板。那么对每个A[i]来说，要求一个最高的左短板，再求一个最高的右短板，这两个直接最短的板子减去A[i]原有的值就是能成多少水了。

所以需要两遍遍历，一个从左到右，找最高的左短板；一个从右到左，找最高的右短板。最后记录下盛水量的总值就是最终结果了。


##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int trap(int[] A) {
       	if(A==null || A.length==0)
       		return 0;
       	int[] leftmax=new int[A.length];
       	int[] rightmax=new int[A.length];
       	int[] container=new int[A.length];
		
		//计算每个bar左边的最大值
       	leftmax[0]=A[0];
       	int max=A[0];
       	for(int i=1;i<A.length;i++)
       	{
       		max=Math.max(max,A[i]);
       		leftmax[i]=max;
       	}

		//计算每个bar右边的最大值
       	rightmax[A.length-1]=A[A.length-1];
       	max=A[A.length-1];
       	for(int i=A.length-2;i>=0;i--)
       	{
       		max=Math.max(max,A[i]);
       		rightmax[i]=max;
       	}

       	int res=0;

       	for(int i=0;i<A.length;i++)
       	{
       		container[i]=Math.min(leftmax[i],rightmax[i])-A[i];
       		res+=container[i];
       	}
       	return res;
    }
}
{% endhighlight %}

[1]:/img/Trapping-Rain-Water/1.png
[2]:http://pisxw.com/algorithm/Candy.html