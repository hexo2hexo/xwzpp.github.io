---
layout: post
title:  LeetCode-Search for a Range
description: "Search for a Range"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Arrays，Binary Search]
duoshuo: true
---
##题目
####Search for a Range 
>Given a sorted array of integers, find the starting and ending position of a given target value.

>Your algorithm's runtime complexity must be in the order of O(log n).

>If the target is not found in the array, return `[-1, -1]`.

>For example,
>Given `[5, 7, 7, 8, 8, 10]` and target value 8,
>return `[3, 4]`.

<!-- more -->

##解题思路
该题可以采用两次二分查找，第一次找到`target`的左边界，第二次找到``target`的右边界。通过相等的时候也向一个方向继续夹逼，如果向右夹逼，最后就会停在右边界，而向左夹逼则会停在左边界，如此用停下来的两个边界就可以知道结果了，只需要两次二分查找。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    //两次二分查找即可
    public int[] searchRange(int[] A, int target) {
        int[] result={-1,-1};
        if(A==null||A.length==0) return result;
        int fl=0;
        int fr=A.length-1;
        while(fl<=fr){
            int mid=(fl+fr)/2;
            if(A[mid]<target)
                fl=mid+1;  //fl表示最左边界
            else
                fr=mid-1;
        }
        
        int sl=0;
        int sr=A.length-1;
        while(sl<=sr){
            int mid=(sl+sr)/2;
            if(A[mid]>target)
                sr=mid-1;  //sr表示最右边界
            else
                sl=mid+1;
        }
        if(fl<=sr)
        {
            result[0]=fl;
            result[1]=sr;
        }
        return result;       
    }
}
{% endhighlight %}
