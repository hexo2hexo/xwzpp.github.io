---
layout: post
title:  LeetCode-Factorial Trailing Zeroes
description: "Majority Element"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math]
duoshuo: true
---
##题目
####Factorial Trailing Zeroes
>Given an integer n, return the number of trailing zeroes in n!.

>Note: Your solution should be in logarithmic time complexity.

>####Credits:
>Special thanks to @ts for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
该题如果像把其结果计算出来后，利用取余的方法求得有多少个0，在这里时间会过不去，因此需要另辟蹊径。

经过分析，发现其零的个数是由5产生的，那么问题就可以解决了，只要求出n中有多少个5不就知道有多少个零了么？举了几个例子试试看，比如n=5，只有一个5，于是结果为result=1，再如n=10，result=2；n=20，result=4。直接举n=100，发现result=24，n / 100 = 20，显然5， 10， 15，...， 95，100，刚好20个数，但是其中还有以下数的因子中有5的倍数，比如25，50， 75，100，这4个数中其实是包含2个5，也就是说就会多产生一个零，于是就有24个了。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int trailingZeroes(int n) {
        //通过分析可知，我们可以对n不断取5模
        if(n<=0)
        	return 0;
        int res=0;
        while(n>=5)
        {
        	n /=5;
        	res+=n;
        }
        return res;
    }
}
{% endhighlight %}






