---
layout: post
title:  LeetCode-Edit Distance
description: "Edit Distance"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming,String]
duoshuo: true
---
##题目
####Edit Distance
>Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.)

>You have the following 3 operations permitted on a word:   

>a) Insert a character   
>b) Delete a character   
>c) Replace a character   

<!-- more -->
	
##解题思路
这道题求一个字符串编辑成为另一个字符串的最少操作数，操作包括添加，删除或者替换一个字符。
这其实是一道二维动态规划的题目，模型上确实不容易看出来，下面我们来说说递推式。   
我们维护的变量res[i][j]表示的是word1的前i个字符和word2的前j个字符编辑的最少操作数是多少。假设我们拥有res[i][j]前的所有历史信息，看看如何在常量时间内得到当前的res[i][j]，我们讨论两种情况：   
1）如果word1[i-1]=word2[j-1]，也就是当前两个字符相同，也就是不需要编辑，那么很容易得到res[i][j]=res[i-1][j-1]，因为新加入的字符不用编辑；   
2）如果word1[i-1]!=word2[j-1]，那么我们就考虑三种操作，如果是插入word1，那么res[i][j]=res[i-1][j]+1，也就是取word1前i-1个字符和word2前j个字符的最好结果，然后添加一个插入操作；如果是插入word2，那么res[i][j]=res[i][j-1]+1，道理同上面一种操作；如果是替换操作，那么类似于上面第一种情况，但是要加一个替换操作（因为word1[i-1]和word2[j-1]不相等），所以递推式是res[i][j]=res[i-1][j-1]+1。上面列举的情况包含了所有可能性，有朋友可能会说为什么没有删除操作，其实这里添加一个插入操作永远能得到与一个删除操作相同的效果，所以删除不会使最少操作数变得更好，因此如果我们是正向考虑，则不需要删除操作。取上面几种情况最小的操作数，即为第二种情况的结果，即res[i][j] = min(res[i-1][j], res[i][j-1], res[i-1][j-1])+1。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int minDistance(String word1, String word2) {
        if(word1.length()==0)  
        	return word2.length();  
    	if(word2.length()==0)  
        	return word1.length();  
        int[][] res=new int[word1.length()+1][word2.length()+1];
        res[0][0]=0;
        for(int i=1;i<=word1.length();i++)//表示word2为空，word1变成word2的删除操作数
            res[i][0]=i;
        for(int j=1;j<=word2.length();j++)//表示word1为空，word2变成word1的删除操作数
            res[0][j]=j;    
        for(int i=1;i<=word1.length();i++)
        {
            for(int j=1;j<=word2.length();j++)
        	{
        		if(word1.charAt(i-1)==word2.charAt(j-1))
        			res[i][j]=res[i-1][j-1];
        		else
        		{
        			int num=Math.min(res[i-1][j],res[i][j-1]);
        			res[i][j]=Math.min(res[i-1][j-1],num)+1;
        		}	
        	}
        }
        
        return res[word1.length()][word2.length()];
    }
}
{% endhighlight %}

