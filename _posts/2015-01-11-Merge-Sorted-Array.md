---
layout: post
title:  LeetCode-Merge Sorted Array
description: "Merge Sorted Array"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Two Pointers]
duoshuo: true
---
##题目
####Merge Sorted Array 
>Given two sorted integer arrays A and B, merge B into A as one sorted array.

>**Note**:    
>You may assume that A has enough space (size that is greater or equal to m + n) to hold additional elements from B. The number of elements initialized in A and B are m and n respectively.

<!-- more -->
	
##解题思路
该题与合并两个有序链表[Merge Two Sorted Lists][1]一样，对每个数组维护一个指针，然后比较指针所指的值，每次迭代中A和B指向的元素大的便加入结果数组中，然后index-1，另一个不动。这里从后往前扫是因为这个题目中结果仍然放在A中，如果从前扫会有覆盖掉未检查的元素的可能性。 

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public void merge(int A[], int m, int B[], int n) {
        if(A==null || B==null)
        	return;
        int index1=m-1;
        int index2=n-1;
        int index3=A.length-1;
        while(index1>=0 && index2>=0)
        {
        	if(A[index1]>B[index2])
        	{
        		A[index3]=A[index1];
        		index3--;
        		index1--;
        	}else{
        		A[index3]=B[index2];
        		index3--;
        		index2--;
        	}	
        }
        while(index2>=0)
        {
        	A[index3]=B[index2];
        	index3--;
        	index2--;
        }
        return;
        	
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Merge-Two-Sorted-Lists.html



