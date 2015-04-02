---
layout: post
title:  LeetCode-Excel Sheet Column Number 
description: "Majority Element"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Math]
duoshuo: true
---
##题目
####Excel Sheet Column Number 
>Related to question [Excel Sheet Column Title][1]

>Given a column title as appear in an Excel sheet, return its corresponding column number.

>For example:
>
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
>####Credits:
>Special thanks to @ts for adding this problem and creating all test cases.

<!-- more -->
	
##解题思路
该题是[Excel Sheet Column Title][1]的翻转，给出字母序列得到对应的单元格数字，这个其实只要找到每一个字母对应的数字，然后乘以其所在的位置的26的次方即可，类似于将字符串数字转化为整数数字。


##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
	public int titleToNumber(String s) {
	    if(s==null ||s.length()==0)
	    	return 0;
	    //用一个map存放26个字母对应的数字
	    HashMap<Character,Integer> map=new HashMap<Character,Integer>();
	    char ch='A';
	    int num=1;
	    map.put(ch,num);
	    while(num<26)
	    {
	    	ch+=1;
	    	num+=1;
	    	map.put(ch,num);
	
	    }
	
	    int res=0;
	    for(int i=0;i<s.length();i++)
	    {
	    	res=res*26+map.get(s.charAt(i));
	    }
	    return res;
	}
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Excel-Sheet-Column-Title.html





