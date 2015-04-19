---
layout: post
title:  LeetCode-Reverse Bits
description: "Reverse Bits"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Bit Manipulation]
duoshuo: true
---
##题目
####Reverse Bits
>Reverse bits of a given 32 bits unsigned integer.

>For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as 00111001011110000010100101000000).

>####Follow up:
>If this function is called many times, how would you optimize it?

>Related problem: Reverse Integer

>####Credits:
>Special thanks to @ts for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
该题的思路与[Reverse Integer][1]类似,这里是对二进制数进行转置，我们可以使用移位的方法进行，对原数不断取最后一位，然后不断右移，而对结果数不断左移或上原数的最后一位。由于位数是确定的，因此只需要移位31次即可。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int res= n & 1;
        for(int i=1;i<=31;i++)
        {
        	n=n>>1; //不断向右移动
        	res=res<<1; //不断向左移动
        	res=res | (n & 1);
        }
        return res;

    }
}
{% endhighlight %}

[1]:pisxw.com/algorithm/leetcode-Reverse-Integer.html








