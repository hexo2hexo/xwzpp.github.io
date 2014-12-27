---
layout: post
title:  LeetCode-Jump Game II 
description: "Jump Game II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Array,Greedy]
duoshuo: true
---
##题目
####Jump Game II
>Given an array of non-negative integers, you are initially positioned at the first index of the array.

>Each element in the array represents your maximum jump length at that position.

>Your goal is to reach the last index in the minimum number of jumps.

>For example:
>Given array A = `[2,3,1,1,4]`k

>The minimum number of jumps to reach the last index is `2`. (Jump `1` step from index 0 to 1, then `3` steps to the last index.)

<!-- more -->
	
##解题思路
该题思想主要是，扫描数组，以确定当前最远能覆盖的节点，放入maxreach。然后继续扫描，直到当前的路程超过了上一次算出的覆盖范围reach，那么更新覆盖范围，同时更新条数，因为我们是经过了多一跳才能继续前进的。

形象地说，这个是在争取每跳最远的greedy.

具体例子可以参考以下[求解博客][1].

常规的DP求解为：

	定义F(i):到第i个元素的最小跳数
	则F(i)=min(F(j))+1,j=0,1,....i-1,且A[j]+j>=i

##算法代码
代码采用JAVA实现：
{% highlight java %}
//第一种方法
public class Solution {
    public int jump(int[] A) {
        if(A==null || A.length==0)
        	return 0;
        int step=0;
        int reach=0;   //已覆盖的位置
        int maxreach=0;  //最大能跳到的位置
         for(int i=0;i<A.length;i++)
        {
        	if(i>reach)
        	{
        		reach=maxreach;
        		step++;
        	}
        	maxreach=Math.max(maxreach,A[i]+i);	
        }
        return step;
    }
}

//第二种方法（常规DP）
public class Solution {
    public int jump(int[] A) {
        if(A==null || A.length==0)
        	return 0;
       	int[] f=new int[A.length];
       	for(int i=0;i<A.length;i++)
       		f[i]=Integer.MAX_VALUE;
       	for(int i=1;i<A.length;i++)
       		for(int j=0;j<i;j++)
       			if((A[j]+j)>=i)
       				f[i]=Math.min(f[i],f[j]+1);
       	return f[A.length-1];
    }
}

{% endhighlight %}

[1]:http://blog.csdn.net/lsdtc1225/article/details/39648757