---
layout: post
title:  LeetCode-Decode Ways
description: "Decode Ways"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,String,Dynamic Programming]
duoshuo: true
---
##题目
####Decode Ways
>A message containing letters from A-Z is being encoded to numbers using the following mapping:
>
	'A' -> 1
	'B' -> 2
	...
	'Z' -> 26

>Given an encoded message containing digits, determine the total number of ways to decode it.

>For example,     
>Given encoded message `"12"`, it could be decoded as `"AB"` (1 2) or `"L"` (12).

>The number of ways decoding `"12"` is 2.

<!-- more -->
	
##解题思路
该题是一个动态规划问题，可以定义如下

	定义：dp[i]表示从第0个元素到第i个元素的解码数
	通过加入第i+1个元素可以看出，i+1个元素只会产生两个结果：
		1. 他自己可以解码，则dp[i+1]=dp[i];
		2. 他与前面一个元素组合起来可以解码，则dp[i+1]=dp[i-1];
	所以dp[i+1]的求解有三种情况：
		1. 他自己可以解码，也可以与前一个元素组合解码
			dp[i+1]=dp[i]+dp[i-1]
		2. 他自己可以解码，不能与前一个元素组合解码
			dp[i+1]=dp[i];
		3. 他自己不能解码，但是能与前一个元素组合解码
			dp[i+1]=dp[i-1]
	自己能够解码：即自己不为字符0
	与前一个元素能够组合解码：即前一个元素不为0且其组合之后不超过26

在代码实现时，需要注意一个小细节，由于需要跨越两个元素，所以当`i=1`时需要特殊处理。

##算法代码
代码采用JAVA实现：     
{% highlight java %}
public class Solution {
    public int numDecodings(String s) {
        if(s==null || s.length()==0)
        	return 0;
        if(s.length()==1 && s.charAt(0)>='1' && s.charAt(0)<='9')
        	return 1;
         if(s.length()==1 && (s.charAt(0)<'1' || s.charAt(0)>'9'))
        	return 0;
        int[] dp=new int[s.length()];//dp[i]表示从第0个字符到第i个字符可以编码的次数
        if(s.charAt(0)=='0')
            dp[0]=0;
        else
            dp[0]=1;
        for(int i=1;i<s.length();i++)
        {
        	boolean one=true;
        	boolean two=true;
        	if(s.charAt(i-1)=='0' || s.charAt(i-1)>'2' || (s.charAt(i-1)=='2' && s.charAt(i)>'6')) 
        	{
        		two=false;  //两位不能解码
        	}
        	if(s.charAt(i)=='0')
        	{
        		one=false;  //一位不能解码
        	}
        	if(two==true && one==true)
        	{
        		dp[i]=(i==1?dp[i-1]+1:dp[i-1]+dp[i-2]);
        	}else if(two==true)
        	{
        		dp[i]=(i==1?1:dp[i-2]);
        	}else if(one==true){
        		dp[i]=dp[i-1];
        	}else{
        		dp[i]=0;
        	}
        }
        return dp[s.length()-1];
    }
}
{% endhighlight %}





