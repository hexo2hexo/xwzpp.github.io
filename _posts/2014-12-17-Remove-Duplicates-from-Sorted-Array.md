---
layout: post
title:  LeetCode-Remove Duplicates from Sorted Array
description: "Remove Duplicates from Sorted Array"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Two Pointers]
duoshuo: true
---
##题目
####Remove Duplicates from Sorted Array
>Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

>Do not allocate extra space for another array, you must do this in place with constant memory.

>For example,
>Given input array `A = [1,1,2]`,

>Your function should return length = `2`, and `A` is now `[1,2]`.

<!-- more -->

##解题思路
该题是去除数组中的多余的重复元素。与[Remove Element][1]类似。做法是维护两个指针，一个保留当前有效元素的长度，一个从前往后扫，然后跳过那些重复的元素。因为数组是有序的，所以重复元素一定相邻，不需要额外记录。时间复杂度是O(n)，空间复杂度O(1)。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int removeDuplicates(int[] A) {
        int len=A.length;
        if(len==0) return 0;
        if(len==1) return 1;
        int i=0,j=1;
        while(j<len){
        	if(A[i]!=A[j])
        	{
        		A[i+1]=A[j];
        		i++;
        		j++;
        	}else{
        		j++;
        	}
        }
        return i+1;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Remove-Element.html