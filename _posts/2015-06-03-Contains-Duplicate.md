---
layout: post
title:  LeetCode-Contains Duplicate
description: "Contains Duplicate"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Hash Table]
duoshuo: true
---
##题目
####Contains Duplicate
>Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct. 

<!-- more -->
	
##解题思路
该题是判断一个数组中是否存在重复的元素，这个思路非常简单，就是利用hash，将数组中的元素存入一个HashMap中，如果存在相同的元素，则会造成冲突。因此可以很容易的判断是否存在重复的元素。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public boolean containsDuplicate(int[] nums) {
        if(nums==null || nums.length==0)
        	return false;
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
        	if(map.containsKey(nums[i]))
        		return true;
        	map.put(nums[i],1);
        }
        return false;
    }
}
{% endhighlight %}















