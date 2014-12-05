---
layout: post
title:  LeetCode-Longest Substring Without Repeating Characters
description: "Longest Substring Without Repeating Characters"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Two Pointers,String]
duoshuo: true
---
##题目
####Longest Substring Without Repeating Characters

>Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

<!-- more -->
##解题思路
该题是求解不包含重复元素的最长字串问题，如果采用“暴力法”求解，时间复杂度为`O(n^3)`,因为每次都要对子串查看是否有元素重复。

本文采用动态规划的方法，假设`A[0]`到`A[i]`的最长不包含重复元素字串长度为`maxsublength`,那么当加入一个元素`A[i+1]`时，需要考虑的是包含`A[i+1]`在内的最长不包含重复元素字串，所以可以通过以`A[i+1]`起始向前搜索而找到,设长度为`length`。在这里，可以通过定义`barrier`表示以`A[i]`为起始，向前搜索而出现第一次重复的位置，这样`A[i+1]`的前向搜索最多只需搜索到`A[barrier+1]`。因此`A[0]`到`A[i+1]`的最长不包含重复元素字串长度为`Max(maxsublength,length)`。

	动态规划的形式化定义如下：
	----------
	length(i)：以A[i]结尾的最长不包含重复元素字串的长度；
	maxlength(i,j):A[i]到A[j]的最长不包含重复元素字串的长度；
	----------
	if i=0 Then maxlength(0,0)=1;
	if i>=1 Then maxlength(0,i)=Max(maxlength(0,i-1),length(i));
	----------
	求解：maxlength(0,A.length);


	
##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    //动态规划
    public int lengthOfLongestSubstring(String s) {
        if(s==null) return 0;
        char[] c=s.toCharArray();
        if(c.length==0) return 0;
        int maxsublength=1;
        int barrier=0;
        for(int i=1;i<c.length;i++)
        {
            for(int j=i-1;j>=barrier;j--)
            {
                if(c[i]==c[j])
                {
                    barrier=j+1;
                    break;
                }
            }
            maxsublength=Math.max(maxsublength,i-barrier+1);
        }
        return maxsublength;     
    }
}
{% endhighlight %}

