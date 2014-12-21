---
layout: post
title:  LeetCode-Search Insert Position
description: "Search Insert Position"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Binary Search]
duoshuo: true
---
##题目
####VSearch Insert Position
>Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

>You may assume no duplicates in the array.

>Here are few examples.  
>`[1,3,5,6]`, 5 → 2  
>`[1,3,5,6]`, 2 → 1  
>`[1,3,5,6]`, 7 → 4  
>`[1,3,5,6]`, 0 → 0   

<!-- more -->

##解题思路
该题是一个对已排序的数组进行元素的插入，但是我们需要知道插入元素的位置信息，因此我们这边可以采用**二分查找**来得到插入的位置信息。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    //利用二分查找
    public int searchInsert(int[] A, int target) {
        if(A==null&&A.length==0) return -1;
        int l=0;
        int r=A.length-1;
        while(l<=r){
            int mid=(l+r)/2;
            if(A[mid]==target)
                return mid;
            if(A[mid]<target){
                l=mid+1;
            }else{
                r=mid-1;
            }
        }
        return l;
    }
}
{% endhighlight %}

[1]:http://sudoku.com.au/TheRules.aspx
[2]:/img/SuDoKu/1.png