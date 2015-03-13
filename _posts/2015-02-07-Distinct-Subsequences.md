---
layout: post
title:  LeetCode-Distinct Subsequences
description: "Distinct Subsequences"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming,String]
duoshuo: true
---
##题目
####Distinct Subsequences
>Given a string S and a string T, count the number of distinct subsequences of T in S.

>A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, `"ACE"` is a subsequence of `"ABCDE"` while `"AEC"` is not).   

>Here is an example:
>S = `"rabbbit"`, T = `"rabbit"`

>Return `3`.

<!-- more -->
	
##解题思路
该题是求`T`的字串在`S`中出现的次数,可以采用动态规划的思想。首先定义维护量res[i][j]:表示S的前i个字符和T的前j个字符有多少个可行的序列。递推式可以定义如下：

	如果S的第i个字符与T的第j个字符不同，则res[i][j]的序列个数应该与res[i-1][j]的个数相同；
	如果S的第i个字符与T的第j个字符相同，那么除了要考虑res[i-1][j-1]的个数情况，还要考虑res[i-1][j]的个数；
	因此，递推式定义如下：
	if(S.charAt(i)==T.charAt(j))
		res[i][j]=res[i-1][j-1]+res[i-1][j];
	else
		res[i][j]=res[i-1][j];

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public int numDistinct(String S, String T) {
        //采用动态规划的思想，定义维护量res[i][j]:表示S的前i个元素和T的前j个元素能够匹配的转化方式
        int[][] res=new int[S.length()+1][T.length()+1];
        if(T.length()==0)
        	return 1;
        if(S.length()==0)
        	return 0;
        //进行初始化
        for(int i=0;i<S.length()+1;i++)
        {
        	res[i][0]=1; //表示当T为空时，不管S长度为多少，只有删除所有元素这一种转化方式
        }

        for(int i=1;i<S.length()+1;i++)
        {
        	for(int j=1;j<T.length()+1;j++)
        	{
        		if(S.charAt(i-1)==T.charAt(j-1))
        		{
        			res[i][j]=res[i-1][j-1]+res[i-1][j];
        		}else{
        			res[i][j]=res[i-1][j];
        		}
        	}
        }

        return res[S.length()][T.length()];
    }
}
{% endhighlight %}








