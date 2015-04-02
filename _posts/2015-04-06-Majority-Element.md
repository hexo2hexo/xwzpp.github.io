---
layout: post
title:  LeetCode-Majority Element
description: "Majority Element"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Divide and Conquer,Array,Bit Manipulation]
duoshuo: true
---
##题目
####Majority Element
>Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

>You may assume that the array is non-empty and the majority element always exist in the array.

>####Credits:
>Special thanks to @ts for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
首先根据超过一半的这个信息，我们可以知道，如果我们对该数组进行排序，那么第`n/2`个数就是所求的那个数。

或者我们仔细观察可以看到，这个元素由于超过一半，那么将它与其余的元素进行相互抵消，则剩下的肯定是我们要找的元素，我们在对数组进行遍历的时候，记录次数，如果否元素次数为0，说明前面正好相互抵消，则令当前元素为起始元素。


##算法代码
代码采用JAVA实现：
方法一：使用排序
{% highlight java %}
public class Solution {
    public int majorityElement(int[] num) {
        if(num==null || num.length==0)
        	return -1;
        Arrays.sort(num);
        return num[num.length/2];
    }
}
{% endhighlight %}

方法二：使用相互抵消，看次数
{% highlight java %}
public class Solution {
    public int majorityElement(int[] num) {
        if(num==null || num.length==0)
        	return -1;
        int nTimes=0;
        int element=0;
        for(int i=0;i<num.length;i++)
        {
        	if(nTimes==0)
        	{
        		element=num[i];
        		nTimes++;
        	}else{
        		if(num[i]==element)
        			nTimes++;
        		else
        			nTimes--;
        	}
        }
        return element;

    }
}
{% endhighlight %}






