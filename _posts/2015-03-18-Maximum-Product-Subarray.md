---
layout: post
title:  LeetCode-Maximum Product Subarray
description: "Maximum Product Subarray"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Dynamic Programming]
duoshuo: true
---
##题目
####Maximum Product Subarray
>Find the contiguous subarray within an array (containing at least one number) which has the largest product.

>For example, given the array `[2,3,-2,4]`,     
>the contiguous subarray `[2,3]` has the largest product = `6`.

<!-- more -->
	
##解题思路
这道题跟[Maximum Subarray][1]模型上和思路上都比较类似，还是用一维动态规划中的“局部最优和全局最优法”。这里的区别是维护一个局部最优不足以求得后面的全局最优，这是由于乘法的性质不像加法那样，累加结果只要是正的一定是递增，乘法中有可能现在看起来小的一个负数，后面跟另一个负数相乘就会得到最大的乘积。不过事实上也没有麻烦很多，我们只需要在维护一个局部最大的同时，在维护一个局部最小，这样如果下一个元素遇到负数时，就有可能与这个最小相乘得到当前最大的乘积和，这也是利用乘法的性质得到的。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int maxProduct(int[] A) {
        if(A==null || A.length==0)
        	return 0;
        if(A.length==1)
            return A[0];
        int global=A[0];
        int maxlocal=A[0];
        int minlocal=A[0];
        for(int i=1;i<A.length;i++)
        {
        	int maxcopy=maxlocal;
        	maxlocal=Math.max(Math.max(maxlocal*A[i],A[i]),minlocal*A[i]);
        	minlocal=Math.min(Math.min(maxcopy*A[i],A[i]),minlocal*A[i]);
        	global=Math.max(global,maxlocal);
        }
        return global;
    }
}
{% endhighlight %}

[1]:





