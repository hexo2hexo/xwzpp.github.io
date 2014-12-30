---
layout: post
title:  LeetCode-Length of Last Word
description: "Length of Last Word"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,String]
duoshuo: true
---
##题目
####Length of Last Word
>Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

>If the last word does not exist, return 0.

>####Note:
> A word is defined as a character sequence consists of non-space characters only.

>For example,    
>Given s = `"Hello World"`,    
>return `5`.   

<!-- more -->
	
##解题思路
该题是找出最后一个单词的长度，由于单词间是用`空格`分割，因此从后往前扫描，并记录单词的长度，但是这里需要注意的是：如果后面都是`空格`，此时还没有找到最后一个单词，应该继续往前找，直到一个非空格字符。那么如果后面再次找到`空格`，说明最后一个单词结束，则可以直接返回最终长度。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public int lengthOfLastWord(String s) {
        char[] schr=s.toCharArray();
        if(s==null || schr.length==0)
        	return 0;
        int res=0;
        for(int i=schr.length-1;i>=0;i--)
        {
        	if(schr[i]!=' ')
        		res++;
        	else{
        		if(res==0)
        			continue;
        		else
        			break;
        	}
        }
        return res;
    }
}
{% endhighlight %}

