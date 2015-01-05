---
layout: post
title:  LeetCode-Combinations
description: "Combinations"
category: algorithm
avatarimg: "/img/leet-code/touxiang.png"
tags : [leetcode,Backtracking]
duoshuo: true
---
##题目
####Combinations
>Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

>For example,
>If n = 4 and k = 2, a solution is:
>
	[
	  [2,4],
	  [3,4],
	  [2,3],
	  [1,2],
	  [1,3],
	  [1,4],
	]  

<!-- more -->
	
##解题思路
该题用到的还是[N-Queens][1]中的方法：用一个循环递归处理子问题。实现的代码跟[Combination Sum][2]非常类似而且更加简练，因为不用考虑重复元素的情况，而且元素只要到了k个就可以返回一个结果.

##算法代码
代码采用JAVA实现：
{% highlight java %}
public class Solution {
    public ArrayList<ArrayList<Integer>> combine(int n, int k) {  
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();  
        if(n<=0 || n<k)  
            return res;  
        helper(n,k,1,new ArrayList<Integer>(), res);  
        return res;  
    }  
    private void helper(int n, int k, int start, ArrayList<Integer> item, ArrayList<ArrayList<Integer>> res)  
    {  
        if(item.size()==k)  
        {  
            res.add(new ArrayList<Integer>(item));  
            return;  
        }  
        for(int i=start;i<=n;i++)  
        {  
            item.add(i);  
            helper(n,k,i+1,item,res);  
            item.remove(item.size()-1);  
        }  
    }
}
{% endhighlight %}

[1]:http://pisxw.com/algorithm/N-Queens.html
[2]:http://pisxw.com/algorithm/Combination-Sum.html