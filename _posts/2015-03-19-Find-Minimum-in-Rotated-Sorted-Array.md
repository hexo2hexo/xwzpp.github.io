---
layout: post
title:  LeetCode-Find Minimum in Rotated Sorted Array
description: "Find Minimum in Rotated Sorted Array"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Binary Search]
duoshuo: true
---
##题目
####Find Minimum in Rotated Sorted Array
>Suppose a sorted array is rotated at some pivot unknown to you beforehand.

>(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

>Find the minimum element.

>You may assume no duplicate exists in the array.

<!-- more -->
	
##解题思路
这道题是[Search in Rotated Sorted Array][1]的扩展，不是找目标元素，而是找最小元素，方法与其类似，首先取中点，然后判断两边哪边有序，如果左边有序，则取左边第一个元素与最小元素进行对比，然后得到更小的元素，再去遍历右边去寻找。否则右边有序，则取右边第一个元素与最小元素进行对比，然后得到更小的元素，再去遍历左边去寻找。每次都能够切掉一半的元素。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int findMin(int[] num) {
        if(num==null || num.length==0)
        	return -1;
        int l=0;
        int r=num.length-1;
        int minnum=Integer.MAX_VALUE;
        while(l<=r)
        {
        	int m=(l+r)/2;
        	//如果左边有序
        	if(num[l]<=num[m])
        	{
        		minnum=Math.min(minnum,num[l]);
        		l=m+1;
        	}
        	else
        	{
        		minnum=Math.min(minnum,num[m]);
        		r=m-1;
        	}
        }
        return minnum;
    }
}
{% endhighlight %}





