---
layout: post
title:  LeetCode-Longest Common Prefix
description: "Longest Common Prefix"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,String]
duoshuo: true
---
##题目
####Longest Common Prefix

>Write a function to find the longest common prefix string amongst an array of strings.

<!-- more -->

##解题思路
该题是求解一个字符串数组的最长公共前缀，这里可以采用“暴力法”，对字符从头开始进行遍历，看是否符合标准，如果不同，则跳出循环返回当前结果，否则继续下一个字符。当然这里可以选取String[0],即第一个字符串作为比较的标准。  
整个算法的时间复杂度应该是`O(m*n)`，`m`表示字符串的最大长度，`n`表示字符串的个数，空间复杂度应该是`O(m)`,即字符串的长度。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
	//以第一个字符串为标准进行比较
    public String longestCommonPrefix(String[] strs) {
        if(strs.length==0) return "";
        if(strs.length==1) return strs[0];
        int offset=0;
        boolean isCommonPrefix=true;
        while(isCommonPrefix)
        {
        	for(int i=0;i<strs.length;i++)
        	{
        		if((offset==strs[i].length())||(strs[i].charAt(offset)!=strs[0].charAt(offset)))
        		{
        			isCommonPrefix=false;
        			break;
        		}
        	}
        	offset+=1;
        }
        return (offset-1)==0?"":strs[0].substring(0,offset-1);
    }
}
{% endhighlight %}

