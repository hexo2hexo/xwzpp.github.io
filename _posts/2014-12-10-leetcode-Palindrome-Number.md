---
layout: post
title:  LeetCode-Palindrome Number
description: "Palindrome Number"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math]
duoshuo: true
---
##题目
####Palindrome Number
>Determine whether an integer is a palindrome. Do this without extra space.

>####Some hints:
>Could negative integers be palindromes? (ie, -1)

>If you are thinking of converting the integer to string, note the restriction of using extra space.

>You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

>There is a more generic way of solving this problem.

<!-- more -->

##解题思路
该题是判断一个整数是不是回文数，即整数逆序翻转之后与原数相同。整数的翻转可以借鉴[LeetCode-Reverse Integer][1]中的方法。这里有一个情况需要考虑，如果整数为负数，则该整数不是回文数。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public boolean isPalindrome(int x) {
        if(x<0) return false;//负数不是回文
        if(x==0) return true;
        //对数值进行翻转，回文翻转之后还等于原来的数
        int reverseNum=0;
        int num=x;
        while(num>0)
        {
        	int modnum=num%10;
        	//考虑翻转会溢出的情况
        	if((reverseNum>Integer.MAX_VALUE/10)||((reverseNum==Integer.MAX_VALUE/10)&&(modnum>Integer.MAX_VALUE%10)))
        		return false;
        	reverseNum=reverseNum*10+modnum;
        	num=num/10;
        }
        if(reverseNum==x)
        	return true;
        else
        	return false;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/leetcode-Reverse-Integer.html