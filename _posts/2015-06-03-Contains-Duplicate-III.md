---
layout: post
title:  LeetCode-Contains Duplicate III
description: "Contains Duplicate III"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Binary Search Tree]
duoshuo: true
---
##题目
####Contains Duplicate III
>Given an array of integers, find out whether there are two distinct indices i and j in the array such that the difference between nums[i] and nums[j] is at most t and the difference between i and j is at most k. 

<!-- more -->
	
##解题思路
该题与[Contains Duplicate][1]和[Contains Duplicate II][2]都不相同，这题主要考察的是两个元素之间的关系。最先想到的思路就是，维持一个长度为k的window, 每次检查新的值是否与原来窗口中的所有值的差值有小于等于t.但是这种方法的时间复杂度为O(nk)，会造成超时。因此需要进行优化。
参考[这篇文章解法][3],发现其使用treeset来存储元素，以达到快速查找元素只差是否小于t的情况，这样时间复杂度为O(nlogk). 


##算法代码
代码采用JAVA实现：
{% highlight java %}
import java.util.SortedSet;  
  
public class Solution {  
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {    
        if(k<1 || t<0 || nums==null) return false;  
          
        SortedSet<Long> set = new TreeSet<Long>();  
          
        for(int j=0; j<nums.length; j++) {  
            SortedSet<Long> subSet =  set.subSet((long)nums[j]-t, (long)nums[j]+t+1);  
            if(!subSet.isEmpty()) return true;  
              
            if(j>=k) {  
                set.remove((long)nums[j-k]);  
            }  
            set.add((long)nums[j]);  
        }  
        return false;  
    }  
}  
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Contains-Duplicate.html
[2]:http://pisxw.com/algorithm/Contains-Duplicate-II.html
[3]:http://blog.csdn.net/xudli/article/details/46323247

















