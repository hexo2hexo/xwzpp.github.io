---
layout: post
title:  LeetCode-Fraction to Recurring Decimal
description: "Fraction to Recurring Decimal"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Math]
duoshuo: true
---
##题目
####Fraction to Recurring Decimal
>Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

>If the fractional part is repeating, enclose the repeating part in parentheses.

>For example,
>
+ Given numerator = 1, denominator = 2, return "0.5".
+ Given numerator = 2, denominator = 1, return "2".
+ Given numerator = 2, denominator = 3, return "0.(6)".
>####Credits:
>Special thanks to @Shangrila for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
先大致介绍一下需要使用到的数据结构，因为要match重复出现过的数据。HashMap必然是首选。记录出现过的数据然后每次检查是否存在在HashMap里面就可以检查重复就好。那么核心问题来了，这个HashSet应该放什么？可能是一个小数循环序列。但是这样子的话首先不说HashSet难以实现，时间复杂度也会很高。如果匹配的是一个小数循环序列，每次都要重新从尾到头遍历一次进行匹配尝试。所以最终的复杂度会是O(N^2)。但是如果存的是每一位对应的余数，就不一样了。先说一下余数的有效性。余数实际上是某种意义的被除数，只要被除数和除数相同，那么商肯定也是一样的。在这里，除数是不变的，所以只要出现了相同的余数/被除数，那么后续的结果序列必然也是相同的。所以实际上我们用一个HashMap<Integer, Integer>即可。键放的是出现过的余数，值放的是对应的位置。所以只要余数出现过一次，再次出现的时候，只要把对应的位置找出来，将左括号插入进去，再在最后加一个右括号就可以了。基于上述讨论，算法如下：

1.先把整数部分解决了。就是大于0的商给算好了。

2。然后从小数部分第一位开始往哈希表里放余数和对应的位置，每次除完之后余数就乘以10相当于往下进一位，同时将当前位的商存入结果。新余数保留做下一个循环使用。

3.循环完结条件有二：1.当前余数已经出现过。表示循环已找到。2.余数变成0，表示这是一个有限循环小数，并没有可以表示的recurring decimal。

4.注意一下边界条件和负数的处理就好。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        //首先先算出整数
        Long long_numerator=(long)numerator;
        long long_denominator=(long)denominator;
        StringBuilder res=new StringBuilder();
        if((double)long_numerator/(double)long_denominator<0)
        	res.append("-");
        res.append(Math.abs(long_numerator/long_denominator));//存放整数部分
        long_numerator %=long_denominator;//余数
        long_numerator *=10;//对余数乘以10，以便进行除法运算。
        if(long_numerator==0)
        	return res.toString();
        res.append(".");

        //定义一个hashmap存放每一位的除数及其在字符串中的位置，如果除数以前出现过，则会出现循环小数,使用long防止溢出
        HashMap<Long,Integer> map=new HashMap<Long,Integer>();
        int cur=res.length();
        while(long_numerator!=0)
        {
        	if(map.containsKey(long_numerator))//如果除数以前出现过，则会出现循环小数
        	{
        		res.append(")");
        		res.insert(map.get(long_numerator),"(");
        		return res.toString();
        	}else{  //如果没有出现过，则继续进行除法运算，直到出现过，或出现0
        		map.put(long_numerator,cur);
        		res.append(Math.abs(long_numerator/long_denominator));
        		long_numerator %=long_denominator;
        		long_numerator *=10;
        		cur++;
        	}
        }
        return res.toString();
    }
}
{% endhighlight %}





