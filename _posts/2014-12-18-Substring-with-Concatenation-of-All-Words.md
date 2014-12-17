---
layout: post
title:  LeetCode-Substring with Concatenation of All Words
description: "Substring with Concatenation of All Words"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Two Pointers,String]
duoshuo: true
---
##题目
####Substring with Concatenation of All Words 
>You are given a string, S, and a list of words, L, that are all of the same length. Find all starting indices of substring(s) in S that is a concatenation of each word in L exactly once and without any intervening characters.

>For example, given:   
S: "barfoothefoobarman"   
L: ["foo", "bar"]

>You should return the indices: [0,9].   
(order does not matter).

<!-- more -->

##解题思路
思路仍然是维护一个窗口，如果当前单词在字典中，则继续移动窗口右端，否则窗口左端可以跳到字符串下一个单词了。假设源字符串的长度为n，字典中单词的长度为l。因为不是一个字符，所以我们需要对源字符串所有长度为l的子串进行判断。做法是i从0到l-1个字符开始，得到开始index分别为i, i+l, i+2*l,的长度为l的单词。这样就可以保证判断到所有的满足条件的串。因为每次扫描的时间复杂度是O(2*n/l)(每个单词不会被访问多于两次，一次是窗口右端，一次是窗口左端)，总共扫描l次（i=0, ..., l-1)，所以总复杂度是O(2*n/l*l)=O(n)，是一个线性算法。空间复杂度是字典的大小，即O(m*l)，其中m是字典的单词数量。

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public List<Integer> findSubstring(String S, String[] L) {
        List<Integer> result=new ArrayList<Integer>();
        if(L.length==0||S.length()==0) return result;
        int wordlen=L[0].length();
        //map中存放L
        HashMap<String,Integer> map=new HashMap<String,Integer>();
        for(int i=0;i<L.length;i++){
            Integer value=map.get(L[i]);
            if(value==null)
                value=1;
            else
                value+=1;
            map.put(L[i],value);
        }

        for(int i=0;i+wordlen<=S.length();i++)
        {
            if(i + wordlen * L.length > S.length()){
                  break;
            }
        	if(map.containsKey(S.substring(i,i+wordlen)))
            {
                boolean b=checkString(S.substring(i,i+wordlen*L.length),new HashMap<String,Integer>(map),wordlen);
                if(b==true)
                    result.add(i);
            }

        }
        return result;
    }

    //检查字符串S是不是map中字符串的组合
    public boolean checkString(String s,HashMap<String,Integer> map,int wordlen)
    {
    	boolean flag=true;
    	int i=0;
    	while(s.length()>0)
    	{
    		String temp=s.substring(0,wordlen);
    		Integer value=map.get(temp);
    		if(value==null||value==0)
    		{
    			flag=false;
    			break;
    		}else{
    			value-=1;
    			map.put(temp,value);
    			s=s.substring(wordlen);
    		}
    			
    	}
    	return flag;
    }
}
{% endhighlight %}
