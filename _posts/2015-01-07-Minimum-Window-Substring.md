---
layout: post
title:  LeetCode-Minimum Window Substring
description: "Minimum Window Substring"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Two Pointers,String]
duoshuo: true
---
##题目
####Minimum Window Substring
>Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

>For example,    
>**S** = `"ADOBECODEBANC"`   
>**T** = `"ABC"`    
>Minimum window is `"BANC"`.    

>**Note**:    
>If there is no such window in S that covers all characters in T, return the emtpy string `""`.    

>If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.   

<!-- more -->
	
##解题思路
这道题是字符串处理的题目，和[Substring with Concatenation of All Words][1]思路非常类似，同样是建立一个字典，然后维护一个窗口，上一题是固定的窗口大小，而这题不是固定的窗口大小，区别是在这道题目中，因为可以跳过没在字典里面的字符，所以遇到没在字典里面的字符可以继续移动窗口右端，而移动窗口左端的条件是当找到满足条件的串之后，一直移动窗口左端直到有字典里的字符不再在窗口里。在实现中就是维护一个HashMap，一开始key包含字典中所有字符，value就是该字符的数量，然后遇到字典中字符时就将对应字符的数量减一。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public String minWindow(String S, String T) {
        if(S==null || T==null ||S.length()==0 ||T.length()==0)
        	return "";
        if(S.length()<T.length())
        	return "";
        int tLength=T.length();
        HashMap<Character,Integer> map=new HashMap<Character,Integer>(); //表示T中的字符是否被包含
        for(int i=0;i<T.length();i++)
        {
        	if(map.containsKey(T.charAt(i)))  
	        {  
	            map.put(T.charAt(i),map.get(T.charAt(i))+1);  
	        }  
	        else  
	        {  
	            map.put(T.charAt(i),1);  
	        }  
        }
       	int start=0; //start ~ end是包含的窗口
       	int end=0;
       	int count=0; //对存在T中的字符进行计数
       	int minstart=0; //最小窗口的起始位置
       	int minlen=S.length()+1;//最小窗口的长度
       	for(;end<S.length();end++)
       	{
       		if(map.containsKey(S.charAt(end)))
       		{
       			map.put(S.charAt(end),map.get(S.charAt(end))-1);
       			if(map.get(S.charAt(end))>=0)  
	            {  
	                count++;  
	            }  
	            while(count==T.length())
	       		{
	       			if(end-start+1<minlen)
	       			{
	       				minlen=end-start+1;
	       				minstart=start;
	       			}
	       			//移动start
	       			if(map.containsKey(S.charAt(start)))
	       			{
	       				map.put(S.charAt(start),map.get(S.charAt(start))+1);
	       				if(map.get(S.charAt(start))>0)  
	                    {  
	                        count--;  
	                    }  
	       			}
	       			start++;
	       		}
       		}
       		
       	}
       	if(minlen>S.length())
       		return "";
       	else
       		return S.substring(minstart,minstart+minlen);
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Substring-with-Concatenation-of-All-Words.html