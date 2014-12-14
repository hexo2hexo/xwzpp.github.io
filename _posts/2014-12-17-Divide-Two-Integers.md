---
layout: post
title:  LeetCode-Divide Two Integers
description: "Divide Two Integers"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math,Binary Search]
duoshuo: true
---
##题目
####Divide Two Integers
>Divide two integers without using multiplication, division and mod operator.

>If it is overflow, return MAX_INT.

<!-- more -->

##解题思路
对于这道题目，因为不能用乘除法和取余运算，我们只能使用位运算和加减法。比较直接的方法是用被除数一直减去除数，直到为0。这种方法的迭代次数是结果的大小，即比如结果为n，算法复杂度是O(n)。 
  
但是这种方法会超时，因此我们不应该每次减去除数，而是尽可能多的减去除数的倍数。而且在做减法的时候，只需考虑两个正数，而结果的正负只需通过看被除数和除数是正是负而得到。

但是这里有溢出的问题需要考虑。如果被除数为`Integer.MIN_VALUE`,则只能加上一个整数才不会发现溢出的问题，因此可以加上`|除数|`，但是结果需要考虑`+1`和`-1`的问题，具体在代码中有所体现。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
	//只能采用加减，移位来求解
    public int divide(int dividend, int divisor) {
        if(dividend==0) return 0;
        if(dividend==Integer.MIN_VALUE)
        {
        	if(divisor<0)
        	{
        		return 1+divide(dividend-divisor,divisor);//相当于原来的结果-1，所以需要+1
        	}else{
        		return divide(dividend+divisor,divisor)-1;
        	}
        }
        if(divisor==0)
        	return Integer.MAX_VALUE;
        if(divisor==Integer.MIN_VALUE)
        	return dividend==divisor ? 1 : 0;
       	if(dividend>0&&divisor<0) return 0-divide(dividend,0-divisor); //总是计算两个整数相除
       	if(dividend<0&&divisor>0) return 0-divide(0-dividend,divisor);
       	if(dividend<0&&divisor<0) return divide(0-dividend,0-divisor);
       	int q=0;
       	int a=1; //a表示r中divisor的个数
       	int r=divisor;
        while(dividend>=divisor)
        {
            if(r>dividend)
            {
                r-=divisor;
                a--;
            }else{
                dividend-=r;
            	q+=a;
            	r+=divisor;
            	a++;
            }
        	
        }
        return q;
    }
}
{% endhighlight %}