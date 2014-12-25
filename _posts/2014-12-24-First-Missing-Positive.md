---
layout: post
title:  LeetCode-First Missing Positive 
description: "First Missing Positive "
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array]
duoshuo: true
---
##题目
####First Missing Positive 
>Given an unsorted integer array, find the first missing positive integer.

>For example,

>Given `[1,2,0]` return `3`,

>and `[3,4,-1,1]` return `2`.

>Your algorithm should run in O(n) time and uses constant space.

<!-- more -->

##解题思路
该题的要求很明确，即第一个不存在的正数，但是需要在线性时间和常量空间下得到。线性的时间意味着不能对数组进行常规排序，因为快排时间复杂度为`O(nlogn)`。常量空间指不能开辟额外的空间。    
因此为了搜寻元素，这里采用数组的下标作为其索引，即对数组的元素进行交换，将正数`i`放到`i-1`的位置上，对于负数和大于数组长度的元素弃之不顾。这样线性扫描一下数组就能得到第一个不存在的正数，即第`j`位置的元素不等于`j+1`。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int firstMissingPositive(int[] A) {
        //将正数放到值-1的位置上，这样1放在0号位置，2放在1号位置，。。。。
        if(A==null || A.length==0)
        	return 1;
        for(int i=0;i<A.length;i++)
        {
        	if(A[i]<=A.length && A[i]>0 && A[A[i]-1]!=A[i])
        	{
        		int temp=A[A[i]-1];
        		A[A[i]-1]=A[i];
        		A[i]=temp;
        		i--;
        	}
        }

        for(int i=0;i<A.length;i++)
        {
        	if(A[i]!=(i+1))
        		return i+1;
        }
        return A.length+1;
    }
}
{% endhighlight %}


