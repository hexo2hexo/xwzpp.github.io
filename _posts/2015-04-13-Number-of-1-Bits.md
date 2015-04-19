---
layout: post
title:  LeetCode-Number of 1 Bits
description: "Number of 1 Bits"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Bit Manipulation]
duoshuo: true
---
##题目
####Number of 1 Bits
>Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

>For example, the 32-bit integer ’11' has binary representation `00000000000000000000000000001011`, so the function should return 3.

>####Credits:
>Special thanks to @ts for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
该题是判断一个数的二进制中1的个数，我们可以通过不断移位，然后判断最后一个数的思想，分别对每位进行判断，如果为1，则将个数+1。最后即可得到1的总个数。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int res=0;
        for(int i=0;i<=31;i++)
	    {
	    	if((n & 1)==1)
	    		res++;
	    	n=n>>1;
	    }
	    return res;
    }
}
{% endhighlight %}










