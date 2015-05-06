---
layout: post
title:  LeetCode-Isomorphic Strings
description: "Isomorphic Strings"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table]
duoshuo: true
---
##题目
####Isomorphic Strings
>Given two strings s and t, determine if they are isomorphic.

>Two strings are isomorphic if the characters in s can be replaced to get t.

>All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

>For example,       
>Given `"egg"`, `"add"`, return true.

>Given `"foo"`, `"bar"`, return false.

>Given `"paper"`, `"title"`, return true.

>####Note:
>You may assume both s and t have the same length.

<!-- more -->
	
##解题思路
该题是判断两个字符串是否是同构的，即两个字符串中的字符是不是存在对应关系。因此我们对每个字符串都设定一个hashmap，在其中存储对应位置两个字符的对应关系，然后我们可以通过判断这种对应关系来解决这个问题。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public boolean isIsomorphic(String s, String t) {
    	//定义两个map分别存储其中元素与另一个字符串元素的对应关系
        HashMap<Character,Character> map_s=new HashMap<Character,Character>();
        HashMap<Character,Character> map_t=new HashMap<Character,Character>();
        for(int i=0;i<s.length();i++)
        {
        	char char_s=s.charAt(i);
        	char char_t=t.charAt(i);
        	//如果该字符没有出现过
        	if(map_s.get(char_s)==null)
        	{
        		if(map_t.get(char_t)!=null)
        			return false;
        		else{
        			//将该两个字符的对应关系进行存储
        			map_s.put(char_s,char_t);
        			map_t.put(char_t,char_s);
        		}
        	}
        	else{
        		if(map_t.get(char_t)==null)
        			return false;
        		else{
        			//如果两个字符都出现过，则需要判断两个字符的对应关系是否是正确的，如果不相互对应，则返回false
        			if(!(map_s.get(char_s)==char_t && map_t.get(char_t)==char_s))
        				return false;
        		}
        	}
        }
        return true;
    }
}
{% endhighlight %}










