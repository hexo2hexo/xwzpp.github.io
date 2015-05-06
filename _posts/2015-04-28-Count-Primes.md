---
layout: post
title:  LeetCode-Count Primes
description: "Count Primes"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Math]
duoshuo: true
---
##题目
####Count Primes
>**Description**:

>Count the number of prime numbers less than a non-negative number, n

>click to show more hints.

>**References**:
>How Many Primes Are There?

>Sieve of Eratosthenes

>**Credits**:
>Special thanks to @mithmatt for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
该方法如果对小于n的每一个数都进行判断的话，会造成超时。因此我们找到更加好的方法进行处理，在这里，我们选择厄拉多塞筛法(Sieve of Eeatosthese)。

该算法的具体操作：先将 2~n 的各个数放入表中，然后在2的上面画一个圆圈，然后划去2的其他倍数；第一个既未画圈又没有被划去的数是3，将它画圈，再划去3的其他倍数；现在既未画圈又没有被划去的第一个数 是5，将它画圈，并划去5的其他倍数……依次类推，一直到所有小于或等于 n 的各数都画了圈或划去为止。这时，表中画了圈的以及未划去的那些数正好就是小于 n 的素数。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int countPrimes(int n) {
        if(n<=2)
        	return 0;
        boolean[] flag=new boolean[n];
        //首先对2进行画圈，然后去除到所有2的倍数
        flag[2]=false;
        for(int i=3;i<n;i++)
        {
        	if(i%2==0)
        		flag[i]=true;
        }

        //对后面第一个没有被去除的数进行画圈，且去除其倍数
        for(int i=3;i<n;i++)
        {
        	if(flag[i]==false)
        	{
        		if(i*i>n)
        			break;
        		else
        		{
        			for(int j=2;j*i<n;j++)
        			{
        				flag[j*i]=true;
        			}
        		}
        	}
        }

        //统计素数的个数
        int res=0;
        for(int i=2;i<n;i++)
        {
        	if(flag[i]==false)
        		res++;
        }

        return res;
    }
}
{% endhighlight %}










