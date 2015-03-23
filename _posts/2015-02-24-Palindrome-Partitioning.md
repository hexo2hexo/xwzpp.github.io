---
layout: post
title:  LeetCode-Palindrome Partitioning
description: "Palindrome Partitioning"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Backtracking]
duoshuo: true
---
##题目
####Palindrome Partitioning
>Given a string s, partition s such that every substring of the partition is a palindrome.

>Return all possible palindrome partitioning of s.    

>For example, given s = "aab",    
>Return    
>
	  [
	    ["aa","b"],
	    ["a","a","b"]
	  ]

<!-- more -->
	
##解题思路 
该题既需要判定每个字串是否为回文串，又要对字符串进行分割，采用循环处理递归子问题的方法，如果当前字串满足回文串，就递归处理字符串剩下的字串，如果到达终点则返回当前结果。

判断字串是否为回文串可以采用[Longest Palindromic Substring][1]中的动态规划的方法求得是否为回文的字典。

##算法代码
代码采用JAVA实现： 
{% highlight java %}
public class Solution {
    public ArrayList<ArrayList<String>> partition(String s) {
        ArrayList<ArrayList<String>> res=new ArrayList<ArrayList<String>>();
        if(s==null || s.length()==0)
        	return res;
        helper(s,isPalindrome(s),0,new ArrayList<String>(),res);
        return res;
    }
	//循环处理子问题
    public void helper(String s,boolean[][] isP,int start,ArrayList<String> cur,ArrayList<ArrayList<String>> res)
    {
    	if(start==s.length())
    	{
    		res.add(new ArrayList<String>(cur));
    		return;
    	}
    	for(int i=start;i<s.length();i++)
    	{
    		if(isP[start][i]==true)
    		{
    			cur.add(s.substring(start,i+1));
    			helper(s,isP,i+1,cur,res);
    			cur.remove(cur.size()-1);
    		}
    	}
    }

    //得到S所有字串的回文情况
    public boolean[][] isPalindrome(String s)
    {
    	boolean[][] res=new boolean[s.length()][s.length()];
    	char[] charS=s.toCharArray();
    	//单个字符
    	for(int i=0;i<charS.length;i++)
    		res[i][i]=true;
    	//两个字符
    	for(int i=0;i<charS.length-1;i++)
    	{
    		if(charS[i]==charS[i+1])
    			res[i][i+1]=true;
    	}
    	//三个以上字符
    	for(int len=3;len<=charS.length;len++)
    	{
    		for(int i=0;i<charS.length-len+1;i++)
    		{
    			if((charS[i]==charS[i+len-1])&&(res[i+1][i+len-1-1]==true))
                {
                    res[i][i+len-1]=true;
                }
    		}
    	}
    	return res;
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/leetcode-Longest-Palindromic-Substring.html









