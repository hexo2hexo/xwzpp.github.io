---
layout: post
title:  LeetCode-String to Integer (atoi)
description: "String to Integer (atoi) "
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math,String]
duoshuo: true
---
##题目
####String to Integer (atoi) 

>Implement atoi to convert a string to an integer.

>Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

>Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

>####Requirements for atoi:
>The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

>The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

>If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

>If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.

<!-- more -->

##解题思路
该题是将字符串转换为整数，但是其中结束条件比较多。需要考虑正负符号问题和整数越界问题。
####该算法的求解步骤如下：

	1. 先去掉多余的空格字符，从第一个非空格字符开始。
	2. 按顺序读数字，如果出现下面三种情况则结束：
		2.1 异常字符出现（按照C语言的标准是把异常字符后面的全部截掉，保留前面的部分作为结果）。
		2.2 数字越界（返回最接近的整数）。
		2.3 字符串结束


##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int atoi(String str) {
        char[] c=str.toCharArray();
        int len=c.length;
        if(len==0) return 0;
        int i=0;
        int sign=1;
        int num=0;
        while(c[i]==' '&&i<len) //从第一个非空格字符开始
        	i++;
        if(i>=len) return 0;
        if(c[i]=='+')   //判断整数的符号，如果没有正负号，则默认为正
        {
        	sign=1;
        	i++;
        }else if(c[i]=='-')
            {
            	sign=-1;
            	i++;
            }
        for(;i<len;i++)
        {
        	if(c[i]<'0'||c[i]>'9') //如果出现异常字符则退出
        		break;
        	if((num>Integer.MAX_VALUE/10)||((num==Integer.MAX_VALUE/10)&&((c[i]-'0')>Integer.MAX_VALUE%10))) //如果出现数值越界，则返回最接近的整数
        	{
        		if(sign==1)
        			return Integer.MAX_VALUE;
        		else
        			return Integer.MIN_VALUE;
        	}
        	num=num*10+(c[i]-'0');
        }
        return sign*num;
    }
}
{% endhighlight %}

