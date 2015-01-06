---
layout: post
title:  LeetCode-Search in Rotated Sorted Array II
description: "Search in Rotated Sorted Array II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Binary Search]
duoshuo: true
---
##题目
####Search in Rotated Sorted Array II
>Follow up for "Search in Rotated Sorted Array":    
>What if duplicates are allowed?   

>Would this affect the run-time complexity? How and why?

>Write a function to determine if a given target is in the array.

<!-- more -->
	
##解题思路
和[Search in Rotated Sorted Array][1]唯一的区别是这道题目中元素会有重复的情况出现。不过正是因为这个条件的出现，出现了比较复杂的case，甚至影响到了算法的时间复杂度。原来我们是依靠中间和边缘元素的大小关系，来判断哪一半是不受rotate影响，仍然有序的。而现在因为重复的出现，如果我们遇到中间和边缘相等的情况，我们就丢失了哪边有序的信息，因为哪边都有可能是有序的结果。假设原数组是{1,2,3,3,3,3,3}，那么旋转之后有可能是{3,3,3,3,3,1,2}，或者{3,1,2,3,3,3,3}，这样的我们判断左边缘和中心的时候都是3，如果我们要寻找1或者2，我们并不知道应该跳向哪一半。解决的办法只能是对边缘移动一步，直到边缘和中间不在相等或者相遇，这就导致了会有不能切去一半的可能。所以最坏情况（比如全部都是一个元素，或者只有一个元素不同于其他元素，而他就在最后一个）就会出现每次移动一步，总共是n步，算法的时间复杂度变成O(n).

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public boolean search(int[] A, int target) {  
    	if(A==null||A.length==0) return false;
        int l=0,r=A.length-1;
        while(l<=r)
        {
            int mid=(l+r)/2;
            if(target==A[mid]) return true;
            if(A[mid]<A[r]){
                if(target>A[mid]&&target<=A[r])
                    l=mid+1;
                else
                    r=mid-1;
            }
            else if(A[mid]>A[r]){
                if(target>=A[l]&&target<A[mid])
                    r=mid-1;
                else
                    l=mid+1;
            }else{
            	r--;
            }
        }
        return false;  
	}  
}
{% endhighlight %}

以上方法和Search in Rotated Sorted Array是一样的，只是添加了中间和边缘相等时，边缘移动一步，但正是这一步导致算法的复杂度由O(logn)变成了O(n).

[1]:http://pisxw.com/algorithm/Search-in-Rotated-Sorted-Array.html

