---
layout: post
title:  LeetCode-Palindrome Partitioning II
description: "Palindrome Partitioning II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming]
duoshuo: true
---
##题目
####Palindrome Partitioning II
>Given a string s, partition s such that every substring of the partition is a palindrome.

>Return the minimum cuts needed for a palindrome partitioning of s.

>For example, given s = `"aab"`,    
>Return `1` since the palindrome partitioning `["aa","b"]` could be produced using 1 cut.
<!-- more -->
	
##解题思路 
该题是只需要求得切割的最小次数，并不需要返回结果信息。因此可以采用动态规划的思想进行求解。   
这道题仍然是动态规划的题目，我们总结一下动态规划题目的基本思路。首先我们要决定要存储什么历史信息以及用什么数据结构来存储信息。然后是最重要的递推式，就是如从存储的历史信息中得到当前步的结果。最后我们需要考虑的就是起始条件的值.    
我们定义如下：

	维护量：dp[i]:表示从第一个字符到第i个字符中切割的最小数。
	递推式：这与这i个字符怎么切隔有关，这里设k为切割位置，可以得到以下递推式：
		if(s(k,i)为回文），则 dp[i+1]=min(dp[i+1],dp[k]+1), 0<=k<=i	
	这里的起始条件为dp[0]=-1

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public int minCut(String s) {
        if(s==null ||s.length()==0)
        	return 0;
        boolean[][] isP=isPalindrome(s);
        //定义维护量
        int[] dp=new int[s.length()+1];
        dp[0]=-1; //起始条件
        for(int i=0;i<s.length();i++)
        {
        	dp[i+1]=i;
        	for(int k=0;k<=i;k++)
 			{
 				if(isP[k][i]==true)
 					dp[i+1]=Math.min(dp[i+1],dp[k]+1);
 			}
        }
        return dp[s.length()];
    }

     //得到S所有字串的回文情况
    public boolean[][] isPalindrome(String s)
    {
    	boolean[][] res=new boolean[s.length()][s.length()];
    	char[] charS=s.toCharArray();
    	//单个字符
    	for(int i=0;i<charS.length;i++)
    		res[i][i]=true;
    	//两个字符
    	for(int i=0;i<charS.length-1;i++)
    	{
    		if(charS[i]==charS[i+1])
    			res[i][i+1]=true;
    	}
    	//三个以上字符
    	for(int len=3;len<=charS.length;len++)
    	{
    		for(int i=0;i<charS.length-len+1;i++)
    		{
    			if((charS[i]==charS[i+len-1])&&(res[i+1][i+len-1-1]==true))
                {
                    res[i][i+len-1]=true;
                }
    		}
    	}
    	return res;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/leetcode-Longest-Palindromic-Substring.html









