---
layout: post
title:  LeetCode-Happy Number
description: "Happy Number"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Math]
duoshuo: true
---
##题目
####Happy Number
>Write an algorithm to determine if a number is "happy".

>A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

>**Example**: 19 is a happy number
>
	1^2 + 9^2 = 82
	8^2 + 2^2 = 68
	6^2 + 8^2 = 100
	1^2 + 0^2 + 0^2 = 1

>####Credits:
>Special thanks to @mithmatt and @ts for adding this problem and creating all test cases.
<!-- more -->
	
##解题思路
该题是判断一个数是不是"Happy Number"，即对其每一位数进行平方和求解，且不断循环这个过程，如果结果为1，则满足条件，如果出现循环的情况，则不满足条件。在这里，采用`HashSet`对过去求解的值进行存储，然后通过判断一个数是不是在其中，来得到是否出现了循环的情况。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public boolean isHappy(int n) {
    	if(n<=0)
       		return false;
       	//使用一个hashset来存储过去已求解的值，来判断是否出现循环
       	HashSet<Integer> set=new HashSet<Integer>();
       	while(n!=1)
       	{
       		n=computerSquare(n);
       		if(set.contains(n))
       			return false;
       		else
       			set.add(n);
       	}
       	return true;
    }
    
    //求一个数的每一位的平方和
    public int computerSquare(int number)
    {
    	int res=0;
    	while(number!=0){
    		int tmp=number%10;
    		number=number/10;
    		res+=tmp*tmp;
    	}
    	return res;
    }
}
{% endhighlight %}










