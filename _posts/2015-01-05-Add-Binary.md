---
layout: post
title:  LeetCode-Add Binary
description: "Add Binary"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math，String]
duoshuo: true
---
##题目
####Add Binary
>Given two binary strings, return their sum (also a binary string).

>For example,    
>a = `"11"`   
>b = `"1"`   
>Return `"100"`.   

<!-- more -->
	
##解题思路
该题是对两个二进制进行求和，这里维护一个进位，分别对`a`和`b`从后往前，每一位进行求和，然后`/2`得到进位，`%2`得到该位的值。如果`a`和`b`长度不一样，则最终还要遍历完长度长的那个字符串。如果最终位也存在进位的情况，则需要将进位放入结果中。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public String addBinary(String a, String b) {
        if(a==null ||a.length()==0)
        	return b;
        if(b==null ||b.length()==0)
        	return a;
        char[] a_char=a.toCharArray();
        char[] b_char=b.toCharArray();
        int jinwei=0;
        int i=a_char.length-1;
        int j=b_char.length-1;
        StringBuilder res=new StringBuilder();  //结果先存在其中，最后通过转置得到结果
        while(i>=0 && j>=0) 
        {
        	int numa=a_char[i]-'0';
        	int numb=b_char[j]-'0';
        	int num=(numa+numb+jinwei)%2;
        	jinwei=(numa+numb+jinwei)/2;
        	res.append(num);
        	i--;
        	j--;
        }
        while(i>=0)  //b字符串已经结束
        {
        	int numa=a_char[i]-'0';
        	int num=(numa+jinwei)%2;
        	jinwei=(numa+jinwei)/2;
        	res.append(num);
        	i--;
        }
        while(j>=0)  //a字符串已经结束
        {
        	int numb=b_char[j]-'0';
        	int num=(numb+jinwei)%2;
        	jinwei=(numb+jinwei)/2;
        	res.append(num);
        	j--;
        }
        if(jinwei!=0)   //最高位存在进位
        	res.append(jinwei);
        res.reverse();
        return res.toString();
    }
}
{% endhighlight %}

