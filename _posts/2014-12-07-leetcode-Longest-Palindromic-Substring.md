---
layout: post
title:  LeetCode-Longest Palindromic Substring
description: "Longest Palindromic Substring"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,String]
duoshuo: true
---
##题目
####Longest Palindromic Substring

>Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

<!-- more -->
##解题思路
该题是求解一个字符串中的最长回文字符串，**回文字符串**的意思是正读和反读都一样的字符串，由于该问题包含最优子结构，因此可以采用**动态规划**的方法求解。

如果`String.length=1`,则该字符串必定是回文字符串。    
如果`String.length=2`,则只有当`String[0]==String[1]`时，该字符串才是回文字符串。
如果`String.length>=3`,则只有当`String[0]==String[String.length-1]且String[1]~String[String.length-2]是回文字符串`，该字符串才是回文字符串。

	动态规划的形式化定义如下：
	-----------
	p[i][j]:字符串中第i位到第j位是否是回文
	-----------
	if i==j Then p[i][i]=true;
	if j-i=1 && c[i]==c[j] Then p[i][j]=true;
	if j-i>=2 && c[i]==c[j] && p[i+1][j-1]==true Then p[i][j]=true;
	-----------
	通过对长度从1到String.length进行遍历，最终就可得到最长的回文字符串。
	
	
##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public String longestPalindrome(String s) {
        char[] c=s.toCharArray();
        int[][] p=new int[c.length][c.length];
        for(int i=0;i<c.length;i++)
            Arrays.fill(p[i],0);
        int startindex=0;
        int maxlong=1;
        for(int i=0;i<c.length;i++)
            p[i][i]=1;
        for(int i=0;i<c.length-1;i++)
        {
            if(c[i]==c[i+1])
            {
               p[i][i+1]=1;
               startindex=i;
               maxlong=2;
            }
                
        }
        for(int len=3;len<=c.length;len++)
        {
            for(int i=0;i<c.length-len+1;i++)
            {
                if((c[i]==c[i+len-1])&&(p[i+1][i+len-1-1]==1))
                {
                    p[i][i+len-1]=1;
                    startindex=i;
                    maxlong=len;
                }
                    
            }
        }
        return s.substring(startindex,startindex+maxlong);      
    }
}
{% endhighlight %}

