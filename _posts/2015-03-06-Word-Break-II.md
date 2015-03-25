---
layout: post
title:  LeetCode-Word Break II
description: "Word Break II"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Dynamic Programming,Backtracking]
duoshuo: true
---
##题目
####Word Break II
>Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

>Return all such possible sentences.

>For example, given       
>s = `"catsanddog"`,       
>dict = `["cat", "cats", "and", "sand", "dog"]`.          

>A solution is `["cats and dog", "cat sand dog"]`.    
>
<!-- more -->
	
##解题思路 
该题与前面[Palindrome Partitioning][1]的解法非常类似,想要获取递归的每种情况，可以采用循环处理递归子问题的方法。分别对单词进行切割，如果满足在字典中，则递归判断下面所有的单词切分，如果不满足，则增加长度，继续判断。

还有一点需要指出的是，下面的代码放到LeetCode中会超时，原因是LeetCode中有一个非常tricky的测试case，其实是不能break的，但是又很长，出现大量的记录和回溯，因此这里可以首先使用上一题`word break`方法进行判断是否有解，然后在进行该代码，这一点我觉得LeetCode没必要把超时设得这么严格，实际意义不大，只是把AC率给拉了下来哈。
##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public ArrayList<String> wordBreak(String s, Set<String> dict) {
        ArrayList<String> res=new ArrayList<String>();
        if(s==null || s.length()==0 || dict==null || dict.size()==0)
        	return res;
        helper(s,0,new ArrayList<String>(),res,dict);
        return res;
    }

    public void helper(String s,int start,ArrayList<String> list,ArrayList<String> res,Set<String> dict)
    {
    	if(start==s.length())
    	{
    		ArrayList<String> newlist=new ArrayList<String>(list);
    		StringBuilder sb=new StringBuilder();
    		for(int i=0;i<newlist.size()-1;i++)
    			sb.append(newlist.get(i)+" ");
    		sb.append(newlist.get(newlist.size()-1));
    		res.add(sb.toString());
    		return;
    	}
    	for(int i=start;i<s.length();i++)
    	{
    		if(dict.contains(s.substring(start,i+1)))
    		{
    			list.add(s.substring(start,i+1));
    			helper(s,i+1,list,res,dict);
    			list.remove(list.size()-1);
    		}
    	}
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/Palindrome-Partitioning.html



