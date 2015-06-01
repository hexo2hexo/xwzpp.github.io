---
layout: post
title:  LeetCode-Kth Largest Element in an Array
description: "Kth Largest Element in an Array"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Divide and Conquer,Heap]
duoshuo: true
---
##题目
####Kth Largest Element in an Array
> Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

>For example,
>Given `[3,2,1,5,6,4]` and k = 2, return 5.

>####Note:
>You may assume k is always valid, 1 ≤ k ≤ array's length.

>####Credits:
>Special thanks to @mithmatt for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
该题的思路在每个算法书里基本上都会有，就是找出一个无序数组中的第k大的元素。

首先最容易想到的就是对这个数组进行排序，然后直接得到结果，但是时间复杂度为O(nlogn)。但是由于我们关心的是第K个，所以没必要对整个数组进行排序，此时我们就会想到快速排序中的partition功能，将一个数组进行分割，得到两个部分，中间元素为x,前一部分元素都小于x,后一部分元素都大于x。根据每一部分的长度，就可以看出第K个元素在哪一部分中。这样一个partition下去，就能得到结果，时间复杂度为O(n)。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
	//可以利用快速排序中的partition来进行求解一个未排序数组中的第K个元素
    public int findKthLargest(int[] nums, int k) {
        return findK(nums,nums.length-k,0,nums.length-1);
    }

    public int findK(int[] nums,int k,int i,int j)
    {
    	if(i>=j) return nums[i];
    	int m=partition(nums,i,j);
    	if(m==k) return nums[m];
    	if(m<k)
    		return findK(nums,k,m+1,j);
    	else
    		return findK(nums,k,i,m-1);
    }

    //快速排序中的partition方法
    public int partition(int[] nums,int i,int j){
    	int x=nums[i];
    	int m=i;
    	int n=i+1;
    	while(n<=j){
    		if(nums[n]<x)
    		{
    			m++;
    			int tmp=nums[m];
    			nums[m]=nums[n];
    			nums[n]=tmp;
    		}
    		n++;
    	}

    	//将x与nums[m]进行互换
    	int tmp=nums[m];
		nums[m]=nums[i];
		nums[i]=tmp;

		return m;

    }


}
{% endhighlight %}















