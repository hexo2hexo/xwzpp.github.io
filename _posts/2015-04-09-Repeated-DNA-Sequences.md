---
layout: post
title:  LeetCode-Repeated DNA Sequences
description: "Repeated DNA Sequences"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Hash Table,Bit Manipulation]
duoshuo: true
---
##题目
####Repeated DNA Sequences
>All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

>Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

>For example,
>
	Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",
	
	Return:
	["AAAAACCCCC", "CCCCCAAAAA"].
<!-- more -->
	
##解题思路
该题首先很容易想到是字符串的匹配问题，可以使用KMP算法，但是如果把所有的长度为10的字串都遍历一遍，然后对每个字串进行模式查找，时间复杂度为O（n^2）.因此需要进行优化，可以发现，其实题目只需要求得那些出现次数多余1次的字串，也就是说我们可以使用“哈希”map进行存储，键为字符串，值为出现的次数，这样对所有长度为10的字串进行便利后，就可以得到每个字串的出现次数，然后在map中找出出现次数大于1的那些字串即可。

结果发现超内存

超内存的原因是什么？肯定是map中的第一个字段，它是字符串，肯定需要很多空间。能不能换个思维，把字符串哈希一下，哈希成可以用比较小的空间就能表示的？因为可能出现的字符只有四种：AGCT，那么这么设计哈希函数：A->0,C->1,G->2,T->3。如此一来，把长度为10的字符串映射（哈希）成整数。

##算法代码
代码采用JAVA实现：
**该代码超内存**
{% highlight java %}
public class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
    	ArrayList<String> res=new ArrayList<String>();
        if(s==null || s.length()==0)
        	return res;
        //定义个hashmap,key为字符串，value为该字符串出现的次数
        HashMap<String,Integer> map=new HashMap<String,Integer>();
        //对所有长度为10的字串进行遍历
        for(int i=0;i<=s.length()-10;i++)
        {
        	String cur=s.substring(i,i+10);
        	if(!map.containsKey(cur))
        	{
        		map.put(cur,1);
        	}else{
        		map.put(cur,map.get(cur)+1);
        	}
        }
        //选出那些出现次数大于1次的那些字符串
       Iterator iterator = map.keySet().iterator();
		while(iterator.hasNext()) {
			String key=(String)iterator.next();
			int val=map.get(key);
			if(val>1)
				res.add(key);
		}
        return res;

    }
}
{% endhighlight %}

**修改之后**
{% highlight java %}
public class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
    	ArrayList<String> res=new ArrayList<String>();
        if(s==null || s.length()==0)
        	return res;
        //定义个hashmap,key为字符串转变成的整数，value为该字符串出现的次数
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        //对所有长度为10的字串进行遍历
        for(int i=0;i<=s.length()-10;i++)
        {
        	String cur=s.substring(i,i+10);
        	int curint=change(cur);
        	if(!map.containsKey(curint))
        	{
        		map.put(curint,1);
        	}else{
        		if(map.get(curint)==1)
        			res.add(cur);
        		map.put(curint,map.get(curint)+1);
        	}
        }
        return res;
    }

    public int change(String s){
    	int res=0;
    	for(int i=0;i<s.length();i++)
    	{
    		res*=10;
    		switch(s.charAt(i)){
    			case 'A':{res+=1;break;}
    			case 'C':{res+=2;break;}
    			case 'G':{res+=3;break;}
    			case 'T':{res+=4;break;}
    		}
    	}
    	return res;
    }
}
{% endhighlight %}







