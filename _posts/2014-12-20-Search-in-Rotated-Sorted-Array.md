---
layout: post
title:  LeetCode-Search in Rotated Sorted Array
description: "Search in Rotated Sorted Array"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Arrays,Binary Search]
duoshuo: true
---
##题目
####Search in Rotated Sorted Array
>Suppose a sorted array is rotated at some pivot unknown to you beforehand.

>(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

>You are given a target value to search. If found in the array return its index, otherwise return -1.

>You may assume no duplicate exists in the array.

<!-- more -->

##解题思路
该题依旧是二分查找的变形，具体来说，假设数组是A，每次左边缘为l，右边缘为r，还有中间位置是m。在每次迭代中，分三种情况：   
（1）如果target==A[m]，那么m就是我们要的结果，直接返回；   
（2）如果A[m]<A[r]，那么说明从m到r一定是有序的（没有受到rotate的影响），那么我们只需要判断target是不是在m到r之间，如果是则把左边缘移到m+1，否则就target在另一半，即把右边缘移到m-1。   
（3）如果A[m]>=A[r]，那么说明从l到m一定是有序的，同样只需要判断target是否在这个范围内，相应的移动边缘即可。   

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int search(int[] A, int target) {
        if(A==null||A.length==0) return -1;
        int l=0,r=A.length-1;
        while(l<=r)
        {
            int mid=(l+r)/2;
            if(target==A[mid]) return mid;
            if(A[mid]<A[r]){
                if(target>A[mid]&&target<=A[r])
                    l=mid+1;
                else
                    r=mid-1;
            }
            else{
                if(target>=A[l]&&target<A[mid])
                    r=mid-1;
                else
                    l=mid+1;
            }
        }
        return -1;
    }
}
{% endhighlight %}
