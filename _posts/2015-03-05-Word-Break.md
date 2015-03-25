---
layout: post
title:  LeetCode-Word Break 
description: "Word Break"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming]
duoshuo: true
---
##题目
####Word Break
>Given a string s and a dictionary of words dict, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

>For example, given      
>s = `"leetcode"`,     
>dict = `["leet", "code"]`.        

>Return true because `"leetcode"` can be segmented as `"leet code"`.

<!-- more -->
	
##解题思路 
该题与前面[Palindrome Partitioning II][1]的解法非常类似，一个试求是否为回文，一个试求是否在字典中。因此这里可以采用动态规划的方法求解

	定义维护量：dp[i]:表示从第一个元素到第i个元素是否能够被切分成字典中的单词组合
	递归式：
         dp[i]=dp[i] || (dp[k-1] && dict.contains(s.substring(k-1,i)));

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public boolean wordBreak(String s, Set<String> dict) {
        if(s==null || s.length()==0 || dict==null || dict.size()==0)
        	return false;
        //定义维护量
        boolean dp[]=new boolean[s.length()+1];
        //进行初始化
        dp[0]=true;
        for(int i=1;i<=s.length();i++)
        {
        	for(int k=1;k<=i;k++)
        	{
        		//定义递归式
        		dp[i]=dp[i] || (dp[k-1] && dict.contains(s.substring(k-1,i)));
        	}
        }
        return dp[s.length()];
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Palindrome-Partitioning-II.html



