---
layout: post
title:  LeetCode-Multiply Strings 
description: "Multiply Strings"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math,String]
duoshuo: true
---
##题目
####Multiply Strings
>Given two numbers represented as strings, return multiplication of the numbers as a string.

>Note: The numbers can be arbitrarily large and are non-negative.

<!-- more -->
	
##解题思路
该题需要知道，`m`和`n`位数的乘积，最终结果为`m+n-1`位或是`m+n`位(进位时)。乘法计算中可以发现，结果中第`i`位，应该由第一个字符串中的第`1`位乘以第二个字符串中的第`i`位，第一个字符串中的第`2`位乘以第二个字符串中的第`i-1`位，.......第一个字符串中的第`i`位乘以第二个字符串中的第`1`位,最后累加求得，最后我们取个位上的数值，然后剩下的作为进位放到下一轮循环中。

举个例子：

	1000=1*1000 第4位=第1位*第4位
	1000=10*100 第4位=第2位*第3位
	1000=100*10 第4位=第3位*第2位
	1000=1000*1 第4位=第4位*第1位

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public String multiply(String num1, String num2) {
        if(num1==null || num2==null)
        	return "";
        if(num1.charAt(0)=='0')
        	return "0";
        if(num2.charAt(0)=='0')
        	return "0";
        int num1length=num1.length();
        int num2length=num2.length();
        //分别对两个开始字符串进行转置，便于后面的下标遍历
        num1=new StringBuilder(num1).reverse().toString();
        num2=new StringBuilder(num2).reverse().toString();
        StringBuilder res=new StringBuilder();
        int jinwei=0;
        //从低位开始计算，最后乘积的位数为m+n-1,如果进位则是m+n
        for(int i=0;i<num1length+num2length-1;i++)
        {
        	int multi=jinwei;
        	for(int j=0;j<=i;j++)
        	{     		
        		if(j<num1length && (i-j)<num2length)
        		{
        			multi+=(num1.charAt(j)-'0')*(num2.charAt(i-j)-'0');
        		}
        	}
        	res.append(multi%10);
        	jinwei=multi/10;
        }
        //考虑最后一位是否有进位
        if(jinwei!=0)
        	res.append(jinwei);
        return res.reverse().toString();   	
    }
}	
{% endhighlight %}

