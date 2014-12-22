---
layout: post
title:  LeetCode-Count and Say
description: "Count and Say"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,String]
duoshuo: true
---
##题目
####Count and Say
>The count-and-say sequence is the sequence of integers beginning as follows:
`1, 11, 21, 1211, 111221, ...`

>`1` is read off as `"one 1"` or `11`.  
>`11` is read off as `"two 1s"` or `21`.   
>`21` is read off as `"one 2, then one 1"` or `1211`.   
>Given an integer `n`, generate the `nth` sequence.

>Note: The sequence of integers will be represented as a string.

<!-- more -->

##解题思路
该题是输出上述字符串序列中第`n`个字符串的问题。该题在生成字符串的过程中，需要首先放入元素的出现次数，然后在放入该元素。因此后一个字符串的生成，需要对前一个字符串统计元素的出现次数问题。

在实现的过程中，需要小心最后一个元素有没有放入的问题。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public String countAndSay(int n) {
        if(n<1)
        	return "";
        if(n==1)
        	return "1";
        String cur="1";
        for(int i=2;i<=n;i++)
        {
        	StringBuilder result=new StringBuilder();
	        int count=1;
        	for(int j=1;j<cur.length();j++)
	        {
	    	 	if(cur.charAt(j)==cur.charAt(j-1))  //统计出现次数
	    	 		count++;
	    	 	else{                                //放入结果字符串中
	    	 		result.append(count);
	    	 		result.append(cur.charAt(j-1));
	    	 		count=1;
	    	 	}
	        }
			//最后一个字符没有放入结果字符串中
	        result.append(count);
	        result.append(cur.charAt(cur.length()-1));
	        cur=result.toString();
        }
        return cur;      
    }
}
{% endhighlight %}

