---
layout: post
title:  LeetCode-Median of Two Sorted Arrays
description: "Median of Two Sorted Arrays"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Divide and Conquer,Array,Binary Search]
duoshuo: true
---
##题目
####Median of Two Sorted Arrays

>There are two sorted arrays A and B of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log(m+n)).

<!-- more -->
##解题思路
该题是求解两个以排序好的数组中的中位数，一般的想法是我们首先先将这两个数组进行合并，然后在找到其中的中位数，其坐标为`k=(m+n)/2`,但是此时的时间复杂度为`O(m+n)`,不符合题意。因此需要进行优化。

上述问题其实可以看成是**求两个数组中的第K大的数是多少**。基本思想是每次通过查看两个数组的第k/2大的数(假设为`A[k/2]`和`B[k/2]`),如果`A[k/2]=B[k/2]`,则说明当前这个数即为两个数组中的第k大的数，如果`A[k/2]>B[k/2]`,则说明第k大的数肯定不在B的前k/2个元素中，此时则可以不用考虑B的前k/2个元素，同上，如果`A[k/2]<B[k/2]`,则说明第k大的数肯定不在A的前k/2个元素中，此时则可以不用考虑A的前k/2个元素，这样每次可以排除k/2个元素，最终k=1时即为结果。  
整个算法的时间复杂度为`O(logk)`，由于`k=(m+n)/2`，所以复杂度为`O(log(m+n))`

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {  
    //as表示A的重新起点，bs表示B的重新起点  
    double findKth(int A[],int as,int m,int B[],int bs,int n,int k)
    {
        if(m==0)
            return B[bs+k-1];
        if(n==0)
            return A[as+k-1];
        if(m>n)
            return findKth(B,bs,n,A,as,m,k);
        if(k==1)
            return Math.min(A[as],B[bs]);
        int pa=Math.min((k+1)/2,m),pb=k-pa;
        if(A[as+pa-1]<B[bs+pb-1])
            return findKth(A,as+pa,m-pa,B,bs,n,k-pa);
        else {
            if(A[as+pa-1]>B[bs+pb-1])
                return findKth(A,as,m,B,bs+pb,n-pb,k-pb);
             else 
                return A[as+pa-1];
        }
        
    }
    
    public double findMedianSortedArrays(int A[], int B[]) {
        int m=A.length;
        int n=B.length;
        int s=m+n;
        if(s%2==1)
            return findKth(A,0,m,B,0,n,s/2+1);
        else
            return (findKth(A,0,m,B,0,n,s/2)+findKth(A,0,m,B,0,n,s/2+1))/2;
    }
}
{% endhighlight %}

