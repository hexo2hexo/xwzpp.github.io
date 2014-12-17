---
layout: post
title:  LeetCode-Implement strStr()
description: "Implement strStr()"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Two Pointers,String]
duoshuo: true
---
##题目
####Implement strStr() 
>Implement strStr().

>Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

####Update (2014-11-02):
>The signature of the function had been updated to return the index instead of the pointer. If you still see your function signature returns a char * or String, please click the reload button  to reset your code definition.

<!-- more -->

##解题思路
这是算法中比较经典的问题，判断一个字符串是否是另一个字符串的子串。这个题目最经典的算法应该是KMP算法，不了解的同学可以看[从头到尾彻底理解KMP][1],里面讲的很清楚。KMP算法是最优的线性算法，复杂度已经达到这个问题的下限。但是KMP算法比较复杂，很难在面试的短时间里面完整正确的实现

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
	//字符串中查找字串，采用KMP算法	
    public int strStr(String haystack, String needle) {
        char[] hay=haystack.toCharArray();
        char[] need=needle.toCharArray();
        if(hay.length==0&&need.length==0) return 0;
        if(hay.length==0) return -1;
        if(need.length==0) return 0;
        if(need.length>hay.length) return -1;
        int i=0;
        //求取needle的next数组
        int[] next=new int[need.length];
        next[0]=-1;
        int j=0;
        int k=-1;
        while(j<need.length-1)
        {
        	if(k==-1||need[j]==need[k])
        	{
				j++;
				k++;
				next[j]=k;        		
        	}
        	else
        	{
        		k=next[k];
        	}
        }
        j=0;
        while(i<hay.length)
        {
        	if(hay[i]==need[j])
        	{
        		i++;
        		j++;
        	}else{
        		j=next[j];
        		if(j==-1)
    		    {
		            i++;
		            j=0;
    		    }
        	}
        	if(j==need.length)
        		break;
        }
        if(j==need.length)
        	return i-need.length;
        else
        	return -1;
    }
}
{% endhighlight %}

[1]:http://blog.csdn.net/v_july_v/article/details/7041827