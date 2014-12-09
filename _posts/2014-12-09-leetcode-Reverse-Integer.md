---
layout: post
title:  LeetCode-Reverse Integer
description: "Reverse Integer"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math]
duoshuo: true
---
##题目
####Reverse Integer

>Reverse digits of an integer.

>Example1: x = 123, return 321

>Example2: x = -123, return -321

>####Have you thought about this?
>Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!

>If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.

>Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?

>For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

<!-- more -->

##解题思路
该题是将给定的整数进行逆序输出，可以通过对10进行取余而得到其个位，十位，百位等。  
但是需要注意以下三个问题：

	1.对于负数的逆序，只需要对其正数进行翻转，然后添加符号即可。
	2.类似于100这样的数，最后的结果应该是1，而不是001.
	3.逆转之后可能会产生比原数更大的数，从而造成整数的溢出。


##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int reverse(int x) {
        if(x==0) return 0;
        if(x<0) return -reverse(-x);
        //每次取模相加，考虑到末尾为0的情况
        int reverseNum=0;
        int modnum=0;
        while(x>0)
        {
            modnum=x%10;
            //考虑翻转会溢出的情况
            if((reverseNum>Integer.MAX_VALUE/10)||((reverseNum==Integer.MAX_VALUE/10)&&(modnum>Integer.MAX_VALUE%10)))
                return 0;
            reverseNum=reverseNum*10+modnum;
            x=x/10;
        }
        return reverseNum;
    }
}
{% endhighlight %}

