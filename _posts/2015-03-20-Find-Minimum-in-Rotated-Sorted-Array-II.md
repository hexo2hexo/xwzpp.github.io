---
layout: post
title:  LeetCode-Find Minimum in Rotated Sorted Array II
description: "Find Minimum in Rotated Sorted Array II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Binary Search]
duoshuo: true
---
##题目
####Find Minimum in Rotated Sorted Array II
>Follow up for "Find Minimum in Rotated Sorted Array":      
>What if duplicates are allowed?

>Would this affect the run-time complexity? How and why?          
>Suppose a sorted array is rotated at some pivot unknown to you beforehand.

>(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

>Find the minimum element.

>The array may contain duplicates.

<!-- more -->
	
##解题思路
这道题是[Find Minimum in Rotated Sorted Array][1]的扩展，里面包含了重复元素。

不过正是因为这个条件的出现，影响到了算法的时间复杂度。原来我们是依靠中间和边缘元素的大小关系，来判断哪一半是不受rotate影响，仍然有序的。而现在因为重复的出现，如果我们遇到中间和边缘相等的情况，我们就无法判断哪边有序，因为哪边都有可能有序。假设原数组是{1,2,3,3,3,3,3}，那么旋转之后有可能是{3,3,3,3,3,1,2}，或者{3,1,2,3,3,3,3}，这样的我们判断左边缘和中心的时候都是3，我们并不知道应该截掉哪一半。解决的办法只能是对边缘移动一步，直到边缘和中间不在相等或者相遇，这就导致了会有不能切去一半的可能。所以最坏情况就会出现每次移动一步，总共移动n此，算法的时间复杂度变成O(n)

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
        while(l<=r){
        	int m=(l+r)/2;
        	if(num[l]<num[m])
        	{
        		minnum=Math.min(minnum,num[l]);
        		l=m+1;
        	}else if(num[l]>num[m])
        	{
        		minnum=Math.min(minnum,num[m]);
        		r=m-1;
        	}else{
				/如果l和m相等，则只能对l+1
        		minnum=Math.min(minnum,num[l]);
        		l++;
        	}

        }
        return minnum;
    }
}
{% endhighlight %}





