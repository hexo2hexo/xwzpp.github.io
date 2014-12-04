---
layout: post
title:  LeetCode-TwoSum
description: "two sum"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,HashTable]
duoshuo: true
---
##题目:
###Two Sum
	
>	Given an array of integers, find two numbers such that they add up to a specific target number.

>	The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.
>	Please note that your returned answers (both index1 and index2) are not zero-based.

>	You may assume that each input would have exactly one solution.

>	Input: numbers={2, 7, 11, 15}, target=9  
>	Output: index1=1, index2=2

<!-- more -->

##解题思路
该题是在给定一个数组中，搜索是否存在两个数的和等于给定的值。如果存在，则返回两个数的数组下标。如果采用“暴搜”，则时间复杂度为`O(n^2)`,为了降低时间复杂度，显然是需要在查询方面做文章，因此可以采用**散列**存储。  

散列是将给定的值转变为一个数组的下标，即散列码，然后在数组中存放值的List。在JAVA中,散列码的求解采用`HashCode()`函数。具有散列功能的`Collections`容器有以下四种:`HashMap`,`LinkedHashMap`,`HashSet`和`LinkedHashSet`，因此本文采用`HashMap`实现散列功能，使得时间复杂度变为`O(n)`。

##算法代码
代码采用JAVA实现：

{% highlight java  %}   
	public class Solution {  
	    public int[] twoSum(int[] numbers, int target) {  
	   		HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();  
	        for(int i=0;i<numbers.length;i++)   
	        {  
	            map.put(numbers[i],i);  
	        }  
	        for(int i=0;i<numbers.length;i++)  
	        {  
	            int cha=target-numbers[i];  
	            Integer v=map.get(cha);  
	            if(v!=null&&v!=i)  
	            {  
	               return new int[]{i+1,v+1};   
	            }  
	        }  
	        return new int[]{-1,-1};   
	    }  
	}  
{% endhighlight %}


