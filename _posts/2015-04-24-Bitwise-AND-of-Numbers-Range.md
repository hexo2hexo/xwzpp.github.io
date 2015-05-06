---
layout: post
title:  LeetCode-Bitwise AND of Numbers Range
description: "Bitwise AND of Numbers Range"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Bit Manipulation]
duoshuo: true
---
##题目
####Bitwise AND of Numbers Range
>Given a range [m, n] where 0 <= m <= n <= 2147483647, return the bitwise AND of all numbers in this range, inclusive.

>For example, given the range [5, 7], you should return 4.

>####Credits:
>Special thanks to @amrsaqr for adding this problem and creating all test cases.
<!-- more -->
	
##解题思路
这道题的意思是，计算从m到n的非负整数的按位与值。太牛逼了，我想了好久都是计算超时。结果其实就是m和n公共头部。例子中5的二进制为101,7的二进制位111，其公共头部为100。再如，若计算3到5的按位或，3的二进制位11，5的二进制位101，没有公共头部，返回0。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        if(m>n)
       		return 0;
       	int i=0;
       	//通过移位寻找公共的头
       	while(m!=n && m!=0)
       	{
       		m=m>>1;
       		n=n>>1;
       		i++;
       	}
       	return m<<i;
    }
}
{% endhighlight %}










