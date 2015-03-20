---
layout: post
title:  LeetCode-Valid Palindrome
description: "Valid Palindrome"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Two Pointers,String]
duoshuo: true
---
##题目
####Valid Palindrome
>Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

>For example,
>`"A man, a plan, a canal: Panama"` is a palindrome.    
>`"race a car"` is not a palindrome.

>####Note:
>Have you consider that the string might be empty? This is a good question to ask during an interview.

>For the purpose of this problem, we define empty string as valid palindrome.

<!-- more -->
	
##解题思路
该题是判断字符串是否是回文，其实只要定义前后两个指针进行遍历，判断其是否相同。但是可以需要跳过不是字母和数字的字符。因此我们要写一个函数判断他是不是合法字符，而且因为忽略大小写，我们在判断两个字符是不是相同的时候如果是大写，要转成相应的小写字母。

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public boolean isPalindrome(String s) {
        if(s==null || s.length()==0)
        	return true;
        char[] res=s.toCharArray();
        int i=0;
        int j=res.length-1;
        while(i<=j)
        {
        	char c1=res[i];
        	char c2=res[j];
        	if(!isvalid(c1))
        	{
        		i++;
        		continue;
        	}
        	if(!isvalid(c2))
        	{
        		j--;
        		continue;
        	}
        	if(!isSame(c1,c2))
        	{
        		return false;
        	}
        	i++;
        	j--;
        }
        return true;
    }
    //判断是否合法
    public boolean isvalid(char c)
    {
    	if(c>='a' && c<='z' || c>='A' && c<='Z' || c>='0' && c<='9')
    		return true;
    	else
    		return false;
    }

    public boolean isSame(char a,char b)
    {
    	//都转化成小写进行比较
    	if(a>='A' && a<='Z')
    	{
    		a=(char)(a-'A'+'a');
    	}
    	if(b>='A' && b<='Z')
    	{
    		b=(char)(b-'A'+'a');
    	}
    	return a==b;
    }
}
{% endhighlight %}









