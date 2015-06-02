---
layout: post
title:  LeetCode-Contains Duplicate II
description: "Contains Duplicate II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Hash Table]
duoshuo: true
---
##题目
####Contains Duplicate II
>Given an array of integers and an integer k, find out whether there there are two distinct indices i and j in the array such that nums[i] = nums[j] and the difference between i and j is at most k. 

<!-- more -->
	
##解题思路
这道题是[Contains Duplicate][1]的扩展，但是思路依然很简单，只是判断是否存在两个重复的数字之间的索引间隔是否不大于K。对于HashMap而言，其中key为数字，value为该数组所有的数组中的索引。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        if(nums==null || nums.length==0) return false;
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        //其中key为数值，value为其索引位置
        for(int i=0;i<nums.length;i++)
        {
        	if(map.containsKey(nums[i]))
        	{
        		int j=map.get(nums[i]);
        		//只需要判断间隔是否不大于K
        		if(i-j<=k) return true;
        		
        	}
        	map.put(nums[i],i);
        }
        return false;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Contains-Duplicate.html















