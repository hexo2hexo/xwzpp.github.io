---
layout: post
title:  LeetCode-Remove Duplicates from Sorted Array II
description: "Remove Duplicates from Sorted Array II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Two Pointers]
duoshuo: true
---
##题目
####Remove Duplicates from Sorted Array II
>Follow up for "Remove Duplicates":    
>What if duplicates are allowed at most twice?

>For example,   
>Given sorted array A = `[1,1,1,2,2,3]`,   

>Your function should return length = `5`, and A is now `[1,1,2,2,3]`. 

<!-- more -->
	
##解题思路
该题是[Remove Duplicates from Sorted Array][1]的延伸，如果重复元素重复次数多于2次，则可以保留下两个该元素，做法同样是维护两个指针，一个保留当前有效元素的长度，一个从前往后扫，然后可以保留两个的就保留两个，然后跳过那些多余的重复元素。因为数组是有序的，所以重复元素一定相邻，不需要额外记录。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int removeDuplicates(int[] A) {
        if(A==null || A.length==0)
        	return 0;
        int i=0;
        int j=1;
        int num=0; //记录重复元素的个数
        while(j<A.length)
        {
        	if(A[i]!=A[j])
        	{
        		A[++i]=A[j++];
        		num=0;
        	}else if(num==0){ //表示已经有一个重复元素了，可以再加一个
        		A[++i]=A[j++];
        		num++;
        	}else{ //超过两个，后面的重复元素则跳过
        		j++;
        	}
        }
        return i+1;
    }
}
{% endhighlight %}

